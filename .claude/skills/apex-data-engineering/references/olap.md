# OLAP

## Scope
Online analytical processing engines and techniques: cube-style aggregation, real-time OLAP systems (ClickHouse, Druid, Pinot, StarRocks), and serving sub-second analytics at high concurrency.

## Core principles
- OLAP and OLTP diverge on physics: OLAP scans millions of rows to return few aggregates (columnar, vectorized, compression-friendly); OLTP touches few rows with strict consistency (row-oriented, index-driven). One engine doing both well remains rare — HTAP claims deserve benchmarks.
- The real-time OLAP niche is defined by three simultaneous demands: ingestion latency of seconds (streaming inserts), query latency under a second, and high concurrency (100s-1000s QPS for user-facing analytics) — warehouses typically fail the last two, which is why ClickHouse/Druid/Pinot exist.
- Pre-aggregation trades storage and ingest cost for query speed: materialized rollups (ClickHouse AggregatingMergeTree/materialized views, Druid rollup at ingestion, Pinot star-tree indexes) turn billion-row scans into thousand-row lookups — but you must keep raw data for the questions you didn't anticipate.
- Vectorized execution over sorted, sparse-indexed columnar parts (ClickHouse's MergeTree: data sorted by ORDER BY key, sparse primary index marking granules of ~8192 rows) is why these engines scan billions of rows per second per node — design the sort key around your dominant filters.
- Approximate answers are a legitimate tool: HyperLogLog for distinct counts, t-digest/quantile sketches for percentiles give 1-2% error at a fraction of the cost — user-facing dashboards rarely need exact uniques over billions.

## Apex practices
- Choose the ORDER BY/sort key by (low-cardinality filter columns first, then time) and validate with granule/segment-skip stats; a wrong sort key in ClickHouse is a table rewrite, so decide with the top 10 queries in hand.
- Denormalize at ingestion: real-time OLAP engines are weak at large joins by design — flatten dimensions into the fact stream (or use dictionary lookups in ClickHouse) rather than joining at query time.
- Set TTL/tiering policies (hot SSD → cold object storage → delete) per table at creation; real-time analytics data has steep value decay and unmanaged retention becomes the cost line item.
- Load-test at production concurrency, not single-query speed: an engine that runs one query in 80ms may collapse at 500 concurrent dashboard users — concurrency behavior is the differentiator among these systems.

## Pitfalls
- Point updates and deletes as a workload: MergeTree mutations are asynchronous table rewrites, not OLTP updates — model corrections as versioned inserts (ReplacingMergeTree) or upstream fixes.
- Rollup-only ingestion that discards raw events, making every new question ("can we split that by device type?") unanswerable without re-ingesting history.
- Small frequent inserts creating part explosions (ClickHouse "too many parts") — batch inserts to thousands of rows or use async_insert/buffer tables.

## Tools & references
ClickHouse docs (MergeTree internals), Apache Druid and Apache Pinot papers/docs, StarRocks/Apache Doris, "Designing Data-Intensive Applications" ch. 3, DataSketches library for approximate algorithms.
