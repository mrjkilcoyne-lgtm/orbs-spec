# Batch Processing

## Scope
Large-scale scheduled computation over bounded datasets: partitioned reprocessing, backfills, resource sizing, and the functional style that makes batch reliable.

## Core principles
- Treat each batch run as a pure function of (immutable input partitions, code version) → output partition; overwrite the output partition wholly on each run so reruns are safe and deterministic.
- Late-arriving data is structural, not exceptional: reprocess a trailing window (e.g., last 3 days) each run, or partition by event time and re-close partitions when late rows land.
- Backfill capacity is a design constraint: if reprocessing a year of history takes a month, your pipeline is unfixable in practice — parallelize backfills across partitions and keep per-partition runtime bounded.
- Skew dominates batch runtime: one hot key or oversized partition makes 99 tasks finish in minutes and 1 in hours; measure partition-size distribution, not just totals.
- Checkpoint at partition granularity, not job granularity — a 10-hour job that restarts from zero on a transient failure at hour 9 is an operational tax; per-partition success markers make restarts cheap.

## Apex practices
- Size batch windows by SLA math: data latency = schedule interval + runtime + retry budget; if consumers need 2-hour freshness, an hourly job with 45-minute runtime and one retry already misses.
- Write outputs with atomic visibility — write to a temp location and rename/commit (or use table-format commits) so downstream jobs never read partial output.
- Encode the processing date as an explicit parameter (`ds` in Airflow terms) and derive all input/output paths from it; never call `now()` inside batch logic.
- Keep a "poison partition" runbook: ability to mark a bad partition, exclude it from downstream aggregation, and re-emit corrected data with a supersedes marker.

## Pitfalls
- Appending instead of overwriting partitions, so every retry or backfill duplicates data — the single most common batch bug.
- Depending on wall-clock scheduling for correctness ("upstream is always done by 3am") instead of explicit data-availability sensors or events.
- Letting one giant unpartitioned "full refresh" table hide inside an otherwise incremental pipeline, quietly becoming the runtime and cost bottleneck.

## Tools & references
Apache Spark, Hadoop MapReduce lineage (Dean & Ghemawat's MapReduce paper), Airflow/Dagster for scheduling, Beauchemin's "Functional Data Engineering", cloud batch services (AWS Batch, Dataproc).
