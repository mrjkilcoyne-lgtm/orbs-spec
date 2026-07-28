# Serverless & FaaS

## Scope
Functions and managed compute: cold starts, statelessness, event integration, cost model.

## Core principles
- Serverless is an operational trade: you surrender runtime control (cold starts, execution limits, vendor lock) for zero server management and scale-to-zero economics — perfect for spiky/event-driven, questionable for steady high-throughput latency-sensitive.
- Functions are stateless and ephemeral by contract: all state externalized; anything in memory/disk is a cache that may vanish (but is reused across warm invocations — exploit both facts).
- Cold starts are architecture: runtime choice, package size, VPC attachment, and provisioned concurrency determine p99; measure them and decide which paths can tolerate them.
- The event source shapes everything: sync HTTP (caller waits, no retry safety-net), async events (built-in retries + DLQs), streams (ordered, batched, poison-pill blocking) — retry/error semantics differ per source, design per source.
- Cost is per-invocation × duration × memory: the model punishes waiting on I/O at high memory and rewards short, right-sized functions — but at sustained load, containers become cheaper; do the math at 10x projected volume.

## Apex practices
- Initialize connections/clients outside the handler (warm reuse); keep dependencies minimal for cold-start weight.
- Idempotent handlers always — every async source is at-least-once; wire DLQs and alerting on every async function.
- One function per responsibility with least-privilege IAM per function — the serverless security win is granular blast radius; don't build the "lambdalith" without deciding to.
- Use step functions/workflow services for multi-step processes instead of functions invoking functions (invisible chains, compounded timeouts).

## Pitfalls
- Function chains where a queue or workflow was needed: timeout stacking and no failure visibility.
- Connection-per-invocation to a relational DB melting it (use proxies/poolers or HTTP-native data APIs).
- Ignoring concurrency limits until a traffic spike throttles the whole account (shared regional pool).

## Tools & references
AWS Lambda/Cloudflare Workers docs, provisioned concurrency, Step Functions, serverless cost calculators.
