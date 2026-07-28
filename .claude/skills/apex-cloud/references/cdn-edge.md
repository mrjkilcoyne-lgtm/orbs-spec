# CDN & Edge Computing

## Scope
Content delivery networks for latency reduction: caching, edge functions, and geographic failover.

## Core principles
- Latency is dominated by distance (physics doesn't scale) — CDNs position caches close to users, reducing round-trip time.
- Cache invalidation is a hard problem; versioning (immutable URLs with content hashes) is simpler than TTL-based expiration.
- Edge functions (Cloudflare Workers, AWS Lambda@Edge) run close to users but have constraints (cold starts, latency limits, memory) — use for light transformations.
- Geographic routing (route traffic to the nearest region) reduces latency but requires multi-region infrastructure for failover.
- DDoS and bot protection is more efficient at the edge than at the origin (filter attacks before they reach your infrastructure).

## Apex practices
- Use content-hashing for URLs (immutable content never expires) for static assets; set cache headers to max-age=31536000 (1 year).
- Implement cache busting (versioning) for deployments: new assets get new URLs, old assets expire naturally.
- Use edge functions for light-weight transformations (image resizing, request routing, security headers) not for business logic.
- Implement geographic failover at the DNS or load balancer level: health checks detect region failures and route traffic elsewhere.

## Pitfalls
- Setting short TTLs on everything because you're unsure about cache (TTL=5 min is not caching) — understand your content freshness requirements.
- Storing sensitive data in edge caches (they're distributed globally) — cache only non-sensitive, non-PII data.
- Using edge functions for database queries (latency, complexity) — edge functions should be <100ms, not 1s+.

## Tools & references
CloudFront (AWS), Cloud CDN (GCP), Azure CDN, Cloudflare, Fastly, Bunny CDN, edge computing whitepaper, "Web Performance in Action".
