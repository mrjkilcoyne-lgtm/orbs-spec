# Query Optimization

## Scope
Analyzing and tuning slow queries: execution plans, join order, predicate pushdown, and cost-based planning. Making queries run faster without restructuring data.

## Core principles
- Every query has an execution plan (EXPLAIN or equivalent); if you haven't read it, you're guessing. The planner ranks alternatives by estimated cost (I/O, CPU) and picks the cheapest. Your job is to make the right plan cheaper than the wrong one.
- Join order matters enormously: joining small result sets first (filter aggressively with WHERE, then join) is faster than joining large tables then filtering. Planner cardinality estimates determine order; if estimates are wrong, hints or query rewrites help.
- Predicates push down: WHERE conditions applied deep in the plan (at table scan time) beat applying them late (after a join). Most planners do this automatically, but complex expressions and subqueries can block it.
- Statistics (table row counts, column value distributions) steer the planner. Stale stats cause catastrophic plans (the planner thinks a join produces 1 row but gets 1M). Rebuild stats after bulk loads; enable autostats on modifying tables.
- Avoiding N+1: a query in a loop (e.g., "get order, then for each line item get product") is O(N) queries. Replace with a single JOIN and loop in-application, or a subquery. Modern ORMs provide eager loading for this.

## Apex practices
- Use EXPLAIN ANALYZE (PostgreSQL) or actual execution traces to see real row counts, not estimated ones. Surprises (estimate: 100, actual: 100K) signal broken statistics or plan cache stale with data change.
- Rewrite complex WHERE conditions into simpler forms: OR conditions often break indexes (use UNION instead); IN with 1K+ values may trigger sequential scan (consider INNER JOIN to a temp table); LIKE 'prefix%' uses indexes, LIKE '%suffix' doesn't.
- Add filtering earlier (in the WHERE clause) to reduce join input sizes; avoid SELECT * and project only needed columns for large tables (enables index-only scans).
- Use window functions (ROW_NUMBER, LAG, LEAD) instead of self-joins for comparisons and rankings; they're faster and more legible.

## Pitfalls
- Trusting the planner's estimate without checking actual rows (EXPLAIN ANALYZE); then wondering why a "fast" query hangs in production on larger datasets.
- Micro-optimizing a query that runs 100ms once an hour while ignoring a query that runs 1s every second.
- Assuming a query is "just slow" when the real issue is it's running thousands of times due to N+1 in the application.

## Tools & references
PostgreSQL EXPLAIN ANALYZE docs, MySQL ANALYZE TABLE, "SQL Performance Explained" (Winand), query profiling tools (pg_stat_statements, MySQL SLOW_QUERY_LOG), index hints.
