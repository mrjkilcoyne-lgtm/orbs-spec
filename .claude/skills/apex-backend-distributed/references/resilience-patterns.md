# Resilience Patterns

## Scope
Surviving partial failure: timeouts, retries, circuit breakers, bulkheads, graceful degradation.

## Core principles
- Timeouts are the foundation everything else builds on: every network call has one, deadline-propagated end-to-end (caller's remaining budget flows down) — an unbounded call is a thread leak during any downstream slowdown.
- Retries amplify load exactly when the system can least afford it: retry only idempotent operations, with exponential backoff + jitter, capped attempts, and retry budgets (e.g. ≤10% of traffic) — and only at one layer, not every layer.
- Circuit breakers fail fast when a dependency is down: after a failure threshold, stop calling and give it air; half-open probes test recovery — this converts a hang into an immediate, handleable error.
- Bulkheads contain the blast: separate pools/queues/quotas per dependency or tenant, so a slow payment provider can't consume every thread serving the homepage.
- Degrade by design: for each dependency decide the fallback in advance — cached data, default value, reduced feature, honest error — the outage decides for you otherwise.

## Apex practices
- Make the failure matrix explicit per dependency: timeout value, retry policy, breaker thresholds, fallback, and alerting — reviewed like schema changes.
- Load-shed at the door under overload (reject cheap/low-priority work early) — accepting everything and timing out on everything serves no one.
- Test failure paths continuously: fault injection (latency, errors) in staging or production chaos experiments; untested fallbacks fail when finally exercised.
- Watch for metastable failure modes: retry storms, cache-miss stampedes after restarts, thundering-herd recoveries — recovery patterns need the same care as failure patterns.

## Pitfalls
- Retry layers multiplying (client × gateway × mesh × app = 81 attempts from one user click).
- Circuit breakers shared across unrelated endpoints of one host (one bad endpoint blackholes the healthy ones).
- Fallbacks that call the same failing dependency by another path.

## Tools & references
"Release It!" (Nygard), resilience4j/Polly, Envoy retry budgets, AWS builders' library (timeouts/retries/jitter articles).
