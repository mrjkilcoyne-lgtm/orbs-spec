# Microservices

## Scope
Decomposing systems into independently deployable services: boundaries, data ownership, operational cost.

## Core principles
- Microservices trade code complexity for operational complexity; the payoff is independent deploy/scale/ownership — no org need, no payoff.
- Boundaries follow the domain (bounded contexts), not technical layers; a service owns its data — no shared databases, ever.
- Every network hop adds failure modes: design for partial failure from the first call (timeouts, retries, fallbacks).
- Loose coupling means schema contracts and async where possible; a synchronous call chain five services deep is a distributed monolith with extra steps.
- You build it, you run it: a service without an owning team that operates it is orphaned production risk.

## Apex practices
- Start with a modular monolith; extract along proven seams when deploy contention or scaling divergence is real and felt.
- Contract tests between services (consumer-driven) so teams deploy without cross-team regression roulette.
- Standardize the platform layer (observability, deploy, config, auth) so services differ only in business logic.
- Design service-to-service auth and tracing from day one — retrofitting identity propagation across 30 services is brutal.

## Pitfalls
- Entity services (UserService, OrderService as CRUD wrappers) recreating the shared database over HTTP.
- Distributed transactions across services instead of redesigning ownership.
- 50 services, 5 engineers.

## Tools & references
"Building Microservices" (Newman), DDD bounded contexts, Pact (contract testing), platform engineering literature.
