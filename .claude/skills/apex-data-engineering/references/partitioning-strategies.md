# Partitioning Strategies

## Scope
Dividing large datasets for pruning, parallelism, and lifecycle management: partition key selection, cardinality math, bucketing/clustering, and format-native approaches.

## Core principles
- Partitioning serves three distinct masters — query pruning (skip data), operational lifecycle (drop/archive/backfill a partition atomically), and write parallelism — and the best key serves the dominant one; trying to optimize all three with one scheme usually optimizes none.
- Cardinality arithmetic is destiny: partitions = product of distinct values per key. Daily × country × event_type = 365 × 200 × 50 ≈ 3.6M partitions/year — metadata explosion and tiny files. Target partition sizes of at least hundreds of MB to low GB; if a partition holds one file, you over-partitioned.
- Partition on what queries filter, in the order they filter: a table partitioned by date serves "last 7 days" beautifully and "all history for customer X" terribly — for the second pattern you need clustering/sorting within partitions, a different table layout, or an index-like structure.
- Hierarchical folder partitioning (Hive-style `dt=2024-01-01/`) couples physical layout to query syntax; Iceberg's hidden partitioning (partition transforms like `days(ts)`, `bucket(16, id)`) decouples them, so queries on the raw column still prune and layout can evolve without breaking readers.
- Skew is the silent killer: partitioning by a power-law key (customer_id where one tenant is 40% of data) creates one whale partition that dominates every scan and shuffle — hash-bucket the whale, salt it, or isolate it.

## Apex practices
- Derive the scheme from the top-N query WHERE clauses and the retention policy, not from the schema: date partitioning almost always first (it's the universal filter and the retention boundary), then at most one more dimension.
- Pair coarse partitioning with fine ordering: partition by day, sort/cluster within partitions by the secondary filter key (user_id, tenant) so file/granule statistics prune what partitioning can't.
- Audit partition health quarterly: size distribution (p5/p50/p95), file counts per partition, and pruning effectiveness from query logs (bytes scanned / bytes in table) — schemes rot as data and queries drift.
- In Iceberg, use partition evolution deliberately (old data keeps old spec, new data gets new spec) instead of rewriting history when query patterns change.

## Pitfalls
- Partitioning by high-cardinality identity columns (user_id, order_id) directly — millions of tiny partitions; that's what bucketing/hashing is for.
- Query predicates that defeat pruning: filtering on `CAST(partition_col AS ...)` or a function of the partition column scans everything in Hive-style tables — the engine can't prune what it can't statically match.
- Designing for today's data volume: a scheme perfect at 10GB/day drowns at 1TB/day — build in the second-level split (hour, bucket) as a documented evolution path.

## Tools & references
Iceberg partition transforms and evolution docs, Hive/Spark partitioning guides, BigQuery partitioning + clustering docs, Snowflake clustering keys, Kleppmann's DDIA ch. 6 (partitioning).
