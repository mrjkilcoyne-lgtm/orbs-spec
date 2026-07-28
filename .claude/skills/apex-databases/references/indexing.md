# Indexing

## Scope
Building and tuning indexes (B-tree, hash, bitmap, full-text) to accelerate queries and enforce uniqueness. Index selection, maintenance cost, and cardinality awareness.

## Core principles
- An index is a sorted copy of a subset of your data, searchable in O(log N) time instead of O(N). Always ask: "Which queries does this index accelerate?" and "What's the cost of maintaining it on writes?"
- Indexes on columns used in WHERE, JOIN, and ORDER BY clauses make sense; indexes on columns checked in aggregate functions (COUNT) don't speed up the computation. `EXPLAIN PLAN` shows whether your index is actually used.
- Index cardinality matters: indexing a boolean column (two values) helps little; indexing user_id (millions of values) is essential. The DB planner may skip a low-cardinality index and scan the table instead.
- Write amplification: every INSERT/UPDATE/DELETE must update the index, not just the table. 100 indexes mean 100x the write cost per row. Tune aggressively — drop unused indexes.
- Composite indexes (idx on col_a, col_b, col_c) support "leftmost prefix" queries: WHERE col_a=1 AND col_b=2 uses the index; WHERE col_b=2 does not (unless col_a is constant-filtered elsewhere). Order matters; think access patterns first.

## Apex practices
- Start with an index on every foreign key (enables JOIN scans) and every uniqueness constraint. Then profile slow queries and add indexes for their hottest filters.
- Use partial indexes (WHERE active=true) to skip indexing cold data, reducing index size and maintenance. PostgreSQL, SQLite, and MySQL 8.0+ support this.
- Monitor index bloat and fragmentation: B-trees degrade with many UPDATEs and DELETEs. PostgreSQL needs `VACUUM`, MySQL needs `OPTIMIZE TABLE`, others auto-compact. Schedule maintenance windows or use autovacuum.
- Covering indexes (including SELECT columns in the index, not just WHERE columns) avoid table lookups entirely ("index-only scan"). PostgreSQL INCLUDE clause, MySQL via multi-column index — trade index size for query speed.

## Pitfalls
- Indexing every column "just in case," bloating the table, slowing writes, and confusing the query planner.
- Using DESC in index definitions (index on col DESC) when the planner would be fine with ASC — avoid unless you have queries sorting ascending and descending on different columns.
- Assuming unique indexes come for free in joins; they help the planner but don't replace the join condition itself (you still need the ON clause).

## Tools & references
PostgreSQL documentation (indexing chapter, EXPLAIN ANALYZE output), "Use the Index, Luke" (Winand — free online), query execution plans (EXPLAIN), missing-index detection queries.
