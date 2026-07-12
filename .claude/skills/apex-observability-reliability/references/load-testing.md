# Load Testing

## Scope
Simulating production load in a controlled environment to find breaking points: capacity limits, performance degradation, and error behaviors.

## Core principles
- Load testing is different from performance testing: performance testing finds inefficiencies in code, load testing finds limits in infrastructure.
- Ramp-up (gradually increasing load) is more realistic than spike tests; systems often degrade gracefully under ramp-up but catastrophically under spikes.
- Breakpoint (the load at which the system becomes unstable) determines capacity; load testing finds the breakpoint before it happens in production.
- Realistic traffic patterns matter: constant load is unrealistic; real traffic has peaks (spikes), valleys (lulls), and correlation (popular items get hot).
- Load testing in production is risky and requires careful setup (isolated traffic, monitoring, kill switches); staging environments often have different behavior.

## Apex practices
- Use k6, Gatling, or JMeter for load testing; they support realistic traffic patterns and metrics collection.
- Test with realistic request distributions: if your API has endpoints for listing, searching, and purchasing, weight them to match real traffic.
- Measure multiple metrics: throughput (requests/sec), latency (p50, p95, p99), error rate, and resource utilization (CPU, memory, connections).
- Test failure scenarios: what happens when a dependency (database, external API) times out? How do circuit breakers behave?

## Pitfalls
- Load testing only the happy path; error scenarios often have higher latency (retries, backoff).
- Testing locally where there's no network latency; add latency injection (tc command, Locust delays) to simulate production.
- Not testing database capacity; app servers scale horizontally, but databases often don't.

## Tools & references
k6 (Grafana's load testing), Gatling, JMeter, Locust (Python), Artillery, load testing best practices (Grafana), chaos engineering (Gremlin, Chaos Mesh), distributed load generation (k6 Cloud).
