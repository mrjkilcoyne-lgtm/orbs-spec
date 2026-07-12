# PostgreSQL

## Scope
Relational database with advanced features: MVCC (snapshot isolation), partial indexes, JSON, procedural language, and replica tuning. OLTP and analytical workloads.

## Core principles
- MVCC (Multiversion Concurrency Control) means readers and writers don't block each other: every transaction sees a consistent snapshot of data at transaction start, even while other transactions modify rows. No read locks; write conflicts are rare.
- Vacuum is not optional: PostgreSQL marks deleted rows as invisible but doesn't free space automatically. `VACUUM` reclaims table space; `VACUUM ANALYZE` also rebuilds statistics. Autovacuum is usually enabled but monitor for lag (tables growing without bound = vacuum not keeping up).
- Table bloat and index bloat degrade performance silently; a table with 100M rows where 90M are dead costs 10x storage and 10x scan time. Monitor pg_stat_user_tables.n_dead_tup; high values mean vacuum is losing.
- Logical replication vs streaming replication: streaming replicas are physical copies (fast, automatic failover, synchronous option), logical replicas can filter tables/columns and exist in other DBs. Standby replicas are read-only; logical subscribers can be written to.
- PostgreSQL extensions add functionality without forking: PostGIS (spatial), hstore/JSONB (semistructured), pg_trgm (fuzzy matching), pgvector (vector similarity). Extensions are stable and first-class.

## Apex practices
- Use JSONB (not JSON) for semistructured data: it's stored as binary, supports GIN indexes, and has useful operators (containment, path navigation). Store structured data in tables, not JSON-in-columns.
- Set `max_connections` and connection pool size (pgBouncer in transaction pooling mode) based on your workload, not arbitrarily high. Too many connections overwhelm the kernel; connection pooling is essential at scale.
- Enable `log_min_duration_statement` to log all queries slower than N ms; use pg_stat_statements extension to track aggregate query time. Profile before tuning.
- Use `EXPLAIN (ANALYZE, BUFFERS)` to see actual I/O and row counts, and `EXPLAIN (FORMAT JSON)` for programmatic analysis. Query plans are your primary debugging tool.

## Pitfalls
- Not enabling autovacuum or tuning it, letting table bloat explode as writes churn.
- Creating indexes without understanding their use in queries; dropping high-cardinality indexes assumes they're unused.
- Syncing replicas with `synchronous_commit=local` but not monitoring lag; replicas can fall behind and give stale reads without alerting.

## Tools & references
PostgreSQL documentation (VACUUM, replication, EXPLAIN), pgAdmin or other GUI tools, pg_stat_statements and pgBadger for query analysis, "Mastering PostgreSQL" (Dietz), replication monitoring dashboards.
