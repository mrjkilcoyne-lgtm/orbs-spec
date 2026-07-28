# Scale Cliffs

## Scope
Code and designs that work at demo scale and collapse at production scale: N+1s, quadratic algorithms, unbounded growth, fan-out explosions — the failure of extrapolation.

## Core principles
- Performance is a step function, not a slope: systems don't degrade gracefully by default — they hit a cliff (cache stops fitting, table stops fitting in RAM, retry storm passes tipping point) and fall off; the blindspot is testing the slope at n=100 and shipping toward a cliff at n=10⁶.
- N+1 is the archetype because it hides perfectly: one query in the code, N queries at runtime, invisible until the list grows — ORMs manufacture it, tests with 3 fixtures never trigger it, and the fix (eager loading, batching) is trivial once *seen*.
- Big-O blindness is really constant-blindness in reverse: the quadratic nested loop over "small" collections is fine until both collections track user growth — anything O(n²) where n is user-controlled or growth-coupled is a scheduled outage.
- Unbounded anything is a cliff: queues without max depth, caches without eviction, logs without rotation, lists without pagination, retries without caps — every "we'll never have that many" is a bet against your own success.
- Fan-out multiplies quietly: one user action → 3 service calls → each 3 more → 27 downstream requests; celebrities/power-users break fan-out designs (the user with 2M followers, the org with 40k members) because distribution tails are where scale actually lives.

## Detection tests
- For each loop and query: what is n coupled to, and what is n's value for the biggest tenant two years from now?
- Count queries per request in tests (assert on it) — does the count grow with fixture size?
- What is unbounded here (queue, cache, payload, result set), and what happens at 100x?

## Countermeasures
- Test with production-shaped data volumes: a seeded 1M-row database in CI catches what 5 fixtures cannot; load tests sized to projected peak ×3.
- Bound everything at creation time: pagination mandatory on collections, caps on queues/payloads/retries, eviction on caches — the limit you set is a graceful error; the one you don't is an outage.
- Design for the tail case explicitly: identify your "celebrity problem" entity and make it a standing test fixture.

## Tools & references
N+1 detectors (bullet, django-silk), EXPLAIN with realistic row counts, load-testing (k6, Locust), "Systems Performance" (Gregg), USE method.
