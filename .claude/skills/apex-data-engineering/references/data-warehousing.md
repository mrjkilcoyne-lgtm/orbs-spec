# Data Warehousing

## Scope
Designing and operating analytical warehouses (Snowflake, BigQuery, Redshift, Databricks SQL): layered architecture, workload management, and cost/performance economics.

## Core principles
- Cloud warehouses separate storage from compute: storage is pennies per TB, compute is the bill — architecture decisions (materialize vs recompute, cluster sizing, auto-suspend) are cost decisions.
- Layer the warehouse: raw/staging (immutable landed data) → integration/core (conformed, tested models) → marts (consumer-shaped). Consumers query marts only; skipping layers couples dashboards to source-system quirks.
- These engines are columnar and scan-oriented: performance comes from scanning fewer bytes — partition/cluster pruning, column selection, and pre-aggregation — not from indexes (mostly absent) or row-level tricks.
- Workload isolation prevents the classic failure: one analyst's cartesian join starving the CEO dashboard. Use separate warehouses/slots/queues per workload class (ELT vs BI vs ad-hoc vs data science).
- Concurrency and freshness trade off against cost: micro-batching every 5 minutes into a warehouse designed for scans can cost more than the analytics are worth — match load frequency to actual decision cadence.

## Apex practices
- Attribute cost to teams and models from day one (query tags, per-warehouse billing, BigQuery slot reservations); the top 10 queries are typically >50% of spend and usually fixable with clustering or materialization.
- Cluster/sort/partition large fact tables on the dominant filter columns (usually date + a high-selectivity key) and verify pruning with EXPLAIN/query-profile bytes-scanned before and after.
- Use zero-copy clones (Snowflake) or table snapshots for dev/test environments and pre-migration safety, instead of maintaining drifting copies.
- Enforce auto-suspend on idle compute, result caching, and query timeouts; alert on warehouses running >X hours and queries scanning >Y TB.

## Pitfalls
- SELECT * against wide fact tables in BI tools — columnar engines bill/scan per column, and dashboards that need 6 columns read 300.
- Treating the warehouse as an application backend (per-request point lookups, OLTP-style updates) — latency, cost, and lock behavior are all wrong for that job.
- No environment separation: analysts building on top of half-loaded staging tables because everything lives in one database with one role.

## Tools & references
Snowflake/BigQuery/Redshift/Databricks documentation on clustering and workload management, Kimball's Toolkit for the modeling layer, "Fundamentals of Data Engineering" (Reis & Housley), FinOps query-attribution practices.
