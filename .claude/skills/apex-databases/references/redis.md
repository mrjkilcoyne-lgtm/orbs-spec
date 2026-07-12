# Redis

## Scope
In-memory data structure store (strings, hashes, lists, sets, sorted sets, streams). Caching, sessions, real-time counters, and pub/sub messaging.

## Core principles
- Everything is in RAM; data must fit in memory. When it doesn't, you're doing Redis wrong (use Memcached for simple key-value caching, or Cassandra/MongoDB for larger workloads). Working set size matters more than total data size.
- Persistence (RDB snapshots or AOF append-only file) is optional. AOF is safer (every write is journaled) but slower. RDB is fast but can lose recent writes on crash. Neither guarantees durability like a traditional database.
- Expiry (TTL) is built-in: keys can expire automatically. This makes Redis ideal for sessions (auto-cleanup) and caches (bounded size). Set TTL on everything or you'll bloat memory with stale data.
- Lua scripting allows atomic multi-step operations: a script runs to completion without interruption from other clients. This avoids race conditions in operations like "increment and get."
- Redis is single-threaded (one command at a time); long-running operations block everything. Avoid KEYS (scans all keys), SORT (is O(N)), or large DEL operations during traffic. Pipelining batches commands to amortize RTT.

## Apex practices
- Use Redis for high-velocity data (real-time counters, leaderboards, session state) where stale data is acceptable or TTL cleanup is the feature, not a bug.
- Implement circuit breaker pattern for Redis: if it's unavailable, degrade gracefully (hit the primary database or return cached/empty responses). Redis makes systems faster, not more reliable.
- Structure keys thoughtfully (e.g., "user:{id}:sessions" for namespacing) to support eviction policies (ALLKEYS-LRU) and to avoid accidental key collisions.
- Use Redis transactions (WATCH/MULTI/EXEC) or Lua scripts for atomic operations, not client-side retry loops (those have race conditions).

## Pitfalls
- Treating Redis as durable storage for important data (users, transactions). Persistence options aren't strong enough; use a proper database.
- Not setting maxmemory and eviction policy; Redis will crash when it runs out of RAM. Policies: ALLKEYS-LRU (evict least-recently-used), VOLATILE-TTL (evict expiring soonest), etc.
- Blocking operations (BLPOP, BRPOP, SORT) that hang connections; use with care in high-concurrency systems.

## Tools & references
Redis documentation (data structures, Lua scripting, persistence), Redis CLI, RedisInsight (GUI), "Redis in Action" (Carlson), "The Little Redis Book" (Seguin).
