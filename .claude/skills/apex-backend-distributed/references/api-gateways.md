# API Gateways & Edge

## Scope
The front door for APIs: routing, authn offload, transformation, BFFs, and gateway anti-patterns.

## Core principles
- The gateway centralizes what every service would otherwise duplicate: TLS termination, authn (token validation), rate limiting, request logging, CORS — cross-cutting policy, one enforcement point.
- Keep business logic out: the moment the gateway transforms payloads with domain rules, it becomes an unversioned, contested monolith owned by nobody.
- The gateway is a chokepoint by design — which means capacity, HA, and latency budgets are platform-critical; it fails, everything fails.
- Backend-for-Frontend (BFF): per-client-type aggregation layers (mobile/web) owned by the client teams beat one generic gateway trying to serve all shapes.
- AuthN at the edge, authZ in services: the gateway verifies who; whether they can touch resource X requires domain context the edge shouldn't have.

## Apex practices
- Declarative gateway config in version control with CI validation — clickops routing is an outage generator.
- Propagate identity and trace context inward (verified JWT/headers with spoofing protection: strip inbound copies of internal headers).
- Set per-route timeouts/retries/limits, not global defaults; the report endpoint and the health check are not the same beast.
- Use the gateway for API versioning/migration mechanics (header/path routing to service versions) — it's the right layer for traffic-shifting.

## Pitfalls
- The "smart pipe": orchestration and payload mapping accreting until every deploy needs a gateway change.
- Double authentication (gateway and services each doing full validation differently, disagreeing on edge cases).
- One shared gateway config file all teams edit (merge-conflict-driven outages) — per-team route ownership.

## Tools & references
Envoy Gateway/Kong/APISIX, cloud gateways (API Gateway/Apigee), BFF pattern (Newman), Kubernetes Gateway API.
