# Connection Pooling

## Scope
Managing database connections efficiently: reusing connections, limiting concurrent connections, and avoiding connection exhaustion. PgBouncer, HikariCP, and connection pool configuration.

## Core principles
- Creating a new database connection is expensive: TCP handshake (tens of ms), authentication, resource allocation. Reusing connections avoids this overhead. A connection pool maintains a set of pre-connected sockets ready for use.
- Connection limits are enforced by the server (max_connections in PostgreSQL, max_connections in MySQL): you can't create more connections than the server allows. Exhausting the limit blocks new clients (connection refused).
- Pool size (min/max connections) determines the tradeoff: too small = clients wait for available connections (queue time), too large = many idle connections consuming server memory. Typical: min=5, max=20 per application server.
- Connection recycling: connections age and leak resources (held locks, uncommitted transactions, memory). Periodically close and recreate connections (lifetime = a few hours). Stale connections cause cryptic errors.
- Prepared statements and client-side caching: prepared statements are cached by the database server (compiled query plan). If each connection re-parses statements, you lose cache benefits. Connection pooling helps amortize statement cache misses.

## Apex practices
- Use a dedicated pooling layer (PgBouncer for PostgreSQL, ProxySQL for MySQL) between applications and the database. Multiplexes many application connections onto fewer database connections (10:1 ratio typical).
- Set reasonable pool sizes: number of concurrent application requests / number of worker threads. If your app has 100 worker threads and the DB can handle 500 connections, use pool size 50-100 (headroom for spikes).
- Monitor pool metrics: active connections, queued requests, connection age, and recycled connections. Gauge whether the pool size is appropriate (queue depth indicates undersizing).
- Enable connection validation: periodically test idle connections (SELECT 1) to catch stale connections before handing them to clients. Cost is small; avoids "connection reset by peer" during queries.

## Pitfalls
- Setting pool size too small (many clients waiting for connections) or too large (idle connections starve server resources). Monitor and tune empirically.
- Not handling connection failures gracefully: if a connection dies mid-query, the pool should eject it and create a new one, not reuse it. Circuit-breaker pattern helps.
- Holding connections open during long operations (network calls, file I/O); the connection is tied up and unavailable to other clients. Async/await or separate connection for blocking I/O helps.

## Tools & references
PgBouncer (PostgreSQL pooling), HikariCP (Java), SQLAlchemy connection pooling (Python), ProxySQL (MySQL), "Optimal Connection Pooling" (various performance blogs), monitoring pool metrics via instrumentation.
