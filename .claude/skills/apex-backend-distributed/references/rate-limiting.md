# Rate Limiting & Admission Control

## Scope
Protecting systems from overload and abuse: algorithms, distributed enforcement, client contracts.

## Core principles
- Rate limiting serves three distinct goals — abuse prevention, fairness between tenants, overload protection — each wants different keys, limits, and responses.
- Token bucket is the workhorse (steady rate + burst allowance); sliding window counters trade precision for simplicity; fixed windows invite boundary bursts (2x at the edge).
- Limit by the right key: per-user, per-API-key, per-IP (weakest), per-tenant — and layer them; one key dimension is always gameable.
- The response is part of the contract: 429 with Retry-After and rate-limit headers turns rejection into cooperation; silent drops turn clients into retry cannons.
- Local limits don't sum to global limits: distributed enforcement needs shared state (Redis), sticky routing, or accepting approximation — decide, don't discover.

## Apex practices
- Load-shed by priority under real overload: shed cheap/anonymous/retryable traffic first, protect the money path — rate limits alone don't save an already-overloaded server.
- Give clients budgets they can see (headers, dashboards) and idempotency keys so their retries are safe.
- Use concurrency limits (in-flight caps, adaptive/AIMD) alongside rate limits — they respond to actual capacity, not guessed request rates.
- Test the limiter's own cost: a Redis round-trip per request to check limits can become the bottleneck; local token caches with async sync.

## Pitfalls
- One global limit for all endpoints (cheap GET and expensive report generation cost the same token).
- Retry-on-429 client defaults without backoff+jitter creating synchronized waves.
- Rate limiting after expensive work (auth, body parsing) instead of at the cheapest possible layer.

## Tools & references
Token bucket/leaky bucket literature, Stripe rate-limiting blog, Envoy/nginx limit modules, draft IETF RateLimit headers.
