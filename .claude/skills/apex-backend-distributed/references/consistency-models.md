# Consistency Models & CAP

## Scope
The contract between a distributed store and its readers: linearizability to eventual, and choosing deliberately.

## Core principles
- CAP is about partitions only: when the network splits you choose consistency (refuse) or availability (serve maybe-stale); the everyday trade-off is PACELC — else, latency vs consistency.
- The spectrum, strongest to weakest: linearizable (one machine illusion) → sequential → causal (causes precede effects) → session guarantees (read-your-writes, monotonic reads) → eventual. Each step down buys latency/availability.
- Session guarantees are the sweet spot users actually notice: read-your-own-writes and monotonic reads prevent the "my comment vanished" class of bugs at modest cost.
- Consistency is per-operation, not per-system: a sane design uses linearizable writes for the account balance and eventual reads for the activity feed.
- Conflict handling is where weak consistency gets real: last-write-wins silently drops data; CRDTs and explicit merge functions preserve it at design cost.

## Apex practices
- Write the consistency requirement into each API's contract ("this read may lag writes by seconds") — implicit assumptions become incident reports.
- Use causal/session tokens (or sticky reads to primary post-write) to give users read-your-writes over an eventually-consistent backend.
- Test with partition injection (jepsen-style thinking): what does each endpoint return during a split?
- Prefer idempotent, commutative operations — they make weak consistency livable.

## Pitfalls
- Reading from replicas right after writing to the primary and filing "data loss" bugs.
- Believing a database's marketing tier ("strong consistency") without reading which operations it covers.
- LWW timestamps across nodes with clock skew silently reordering causality.

## Tools & references
Jepsen analyses, jepsen.io/consistency map, DDIA ch. 5/9, PACELC paper, cloud DB consistency docs.
