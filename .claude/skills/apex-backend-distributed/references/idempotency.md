# Idempotency

## Scope
Making retries safe: idempotency keys, dedup, natural idempotency in API and consumer design.

## Core principles
- Retries are not optional in distributed systems (timeouts are ambiguous — did it happen?), so idempotency is not optional either: the question is where it's enforced.
- Natural idempotency first: SET x=5, upserts by natural key, state-machine transitions (order: paid→paid is a no-op) — design operations so repetition is harmless.
- Where creation isn't naturally idempotent, use idempotency keys: client sends a unique key, server stores key→result atomically with the effect, replays return the stored result.
- The key store must be atomic with the operation (same transaction/conditional write); check-then-act across two systems just moves the race.
- Scope and expiry are part of the contract: keys per endpoint per client, retained long enough to cover realistic retry windows, with defined behavior on payload mismatch (reject, don't replay).

## Apex practices
- Return the original result on replay (same status, same body) — idempotent means indistinguishable, not "409 conflict, good luck."
- In consumers, dedup by event ID with a processed-set written in the same transaction as the side effect.
- Propagate keys through the chain: a payment API calling a ledger passes derived keys so the whole path is replay-safe.
- Test with a chaos retry harness: fire every mutation twice concurrently and after timeout; the duplicates you find in staging are refunds you don't issue in prod.

## Pitfalls
- Idempotency implemented as a Redis check separate from the DB write (crash between = duplicate).
- Auto-generated UUIDs server-side as the "idempotency key" (defeats the purpose — the client must own it).
- Non-idempotent side effects hiding inside idempotent-looking handlers (metrics, emails, webhook fan-out).

## Tools & references
Stripe idempotency docs (the canon), IETF Idempotency-Key draft, conditional writes (DynamoDB/SQL upsert).
