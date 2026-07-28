# SQL

## Scope
Declarative set-based querying: joins, aggregation, window functions, query semantics.

## Core principles
- Think in sets, not loops: describe the result, let the planner find the path.
- NULL is three-valued logic: `= NULL` is never true; NOT IN with NULLs returns nothing — the classic silent wrong-answer.
- Logical evaluation order (FROM→WHERE→GROUP BY→HAVING→SELECT→ORDER BY) explains what you can reference where.
- Window functions compute over partitions without collapsing rows — the answer to "top N per group" and running totals.
- The schema is the query's destiny: normalization, keys, and constraints determine what queries are even expressible cleanly.

## Apex practices
- CTEs for readable stepwise logic; know when your engine materializes them (fences) vs inlines.
- EXPLAIN before optimizing; read whether the plan matches your mental model (index use, join order, row estimates).
- Write deterministic queries: explicit ORDER BY when order matters, explicit column lists always.
- Use constraints (FK, CHECK, UNIQUE) as executable documentation and last-line data defense.

## Pitfalls
- Implicit cross joins / accidental many-to-many fanout doubling aggregates.
- Functions on indexed columns in WHERE (`WHERE date(created_at)=...`) killing index use.
- SELECT * in production code coupling apps to schema layout.

## Tools & references
Use The Index Luke, modern-sql.com, per-engine EXPLAIN docs, "SQL Antipatterns" (Karwin).
