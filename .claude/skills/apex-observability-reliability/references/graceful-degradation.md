# Graceful Degradation

## Scope
Operating with reduced functionality when systems fail: feature flags, circuit breakers, and fallback modes.

## Core principles
- Graceful degradation (serving requests with reduced functionality) is better than complete failure; a slow search is better than no search.
- Circuit breakers (fail-fast when a downstream dependency is broken) prevent cascading failures; they have states (open, half-open, closed).
- Feature flags (runtime toggling of features) allow immediate rollback without redeployment; they're the foundation of safe operations.
- Fallbacks (serving cached results, using defaults) keep the service alive when dependencies fail.
- Load shedding (rejecting low-priority requests) preserves resources for critical paths when the system is overloaded.

## Apex practices
- Use libraries (Resilience4j, Polly, Istio) for circuit breakers; don't implement them yourself.
- Feature flags should be queryable (what's the current state of each flag?) and auditable (who changed it?).
- Design for cascading failures: when service A depends on B and C, and B fails, what happens? (Should A serve cached data? Should A reject requests?)
- Test degradation scenarios in load tests; verify that fallbacks activate and serve traffic.

## Pitfalls
- Feature flags that are never cleaned up; old flags create technical debt and configuration complexity.
- Circuit breakers that are too sensitive (open on the first error) or too lenient (never open, defeating the purpose).
- Graceful degradation that leaves the system in an inconsistent state (serves old data without indicating staleness).

## Tools & references
Feature flag libraries (LaunchDarkly, Unleash, Harness), circuit breaker libraries (Resilience4j, Polly, Hystrix), Istio (service mesh degradation), load shedding (Netflix Hystrix), chaos testing (Gremlin, Chaos Mesh).
