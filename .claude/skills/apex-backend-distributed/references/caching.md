# Caching

## Scope
Caching at every layer: strategies, invalidation, stampedes, coherence.

## Core principles
- A cache is a bet that reads outnumber changes; every cache adds a staleness contract — write it down (TTL, invalidation trigger).
- The two hard problems are real: invalidation (event-driven beats TTL-guessing) and naming (cache keys must capture every input that affects the value).
- Cache-aside is the default pattern (read: try cache → load → fill; write: invalidate); write-through/behind only with clear consistency reasoning.
- Stampede protection is mandatory at scale: locks/single-flight, probabilistic early refresh, or stale-while-revalidate — or expiry becomes an outage.
- Layered caches multiply: browser → CDN → gateway → app → DB buffer; know what's cached where or debugging becomes archaeology.

## Apex practices
- Include version/tenant/locale in keys; namespace and version key schemas so a deploy can atomically "flush" by prefix.
- Set TTLs with jitter to avoid synchronized expiry; monitor hit ratio and eviction rate per cache.
- Negative caching (cache the 404) with short TTLs to stop miss-storms on nonexistent keys.
- Decide failure mode explicitly: cache down → serve stale, degrade, or pass through — and load-test the pass-through.

## Pitfalls
- Caching authenticated/personalized responses in shared caches (data leak, the classic CDN incident).
- Cache as the source of truth (data that exists only in Redis).
- "Just add Redis" before measuring — a query fix beats a coherence problem.

## Tools & references
Redis/Memcached docs, HTTP caching RFC 9111, stale-while-revalidate, groupcache/single-flight patterns.
