# Apache Spark

## Scope
Distributed compute with Spark: execution model (jobs/stages/tasks), shuffles, memory management, Catalyst/AQE, and tuning DataFrame/SQL workloads.

## Core principles
- Everything reduces to shuffles: Spark splits a job into stages at shuffle boundaries (wide dependencies — groupBy, join, repartition). Minimizing and shrinking shuffles is 80% of Spark tuning; narrow transformations are nearly free.
- Lazy evaluation means the plan, not your code, executes: Catalyst rewrites DataFrame/SQL logic (predicate pushdown, column pruning, join reordering), so read `explain()` output — the physical plan — when performance surprises you.
- Partitions are the unit of parallelism and of failure: too few starves the cluster, too many drowns it in scheduling overhead; target task durations of roughly 100ms-2s and partition sizes near 128MB post-shuffle.
- Skew breaks the averages: one hot key makes a single task process gigabytes while the rest idle. Adaptive Query Execution (AQE, default since 3.2) auto-splits skewed shuffle partitions and coalesces small ones — keep it on and verify it fired.
- Memory is split between execution (shuffles, joins, sorts) and storage (cache) under unified memory management; spills to disk are the symptom to watch, and OOM usually means skew, oversized broadcast, or collect() — not "add more RAM."

## Apex practices
- Broadcast the small side of joins (Spark auto-broadcasts under `spark.sql.autoBroadcastJoinThreshold`, default 10MB — raise it deliberately for known-small dims) to eliminate the shuffle entirely.
- Use the Spark UI as the primary debugger: stage timeline for stragglers, shuffle read/write sizes per task for skew, spill metrics for memory pressure — before touching any config knob.
- Prefer built-in SQL functions and DataFrame ops over Python UDFs (which serialize row-by-row through the JVM/Python boundary); when UDFs are unavoidable, use pandas/Arrow-vectorized UDFs.
- Control output file counts explicitly (`coalesce`/`repartition` before write, or AQE coalescing) — default parallelism writing 200 files per partition creates the small-files problem downstream.

## Pitfalls
- `collect()` or `toPandas()` on a large DataFrame, driving the entire dataset through the driver's heap.
- Repeatedly recomputing an expensive lineage because nothing was cached/checkpointed — or the opposite, caching everything and evicting the one DataFrame that mattered.
- groupByKey-style patterns (collecting all values per key) where reduce/agg-style incremental aggregation would keep memory bounded.

## Tools & references
Spark UI and `explain()`, "Spark: The Definitive Guide" (Chambers & Zaharia), "Learning Spark" 2nd ed., the Zaharia RDD paper (NSDI 2012), Spark SQL tuning guide (AQE docs).
