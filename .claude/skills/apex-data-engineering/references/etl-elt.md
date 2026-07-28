# ETL / ELT

## Scope
Moving and transforming data between systems: extract patterns, load strategies, ELT-in-warehouse vs ETL-in-flight, and pipeline idempotency.

## Core principles
- ELT won because warehouses got cheap and elastic: land raw data first, transform with SQL inside the warehouse, keep raw immutable — you can always re-derive, you can never re-extract the past.
- Every pipeline run must be idempotent: re-running for the same input window yields the same output (delete+insert by partition, MERGE on keys, or overwrite) — retries and backfills are the normal case, not the exception.
- Incremental extraction needs a reliable watermark (updated_at with late-arrival slack, log sequence number, or CDC offset); "rows since last run's wall-clock time" silently drops rows written during the run.
- Separate extraction from transformation from loading as independently retryable steps with persisted intermediate state; a monolithic script that does all three re-extracts everything when the last step fails.
- Data contracts at ingestion beat cleanup downstream: validate schema, nullability, and enum domains at the boundary, quarantine violations to a dead-letter table instead of failing or silently coercing.

## Apex practices
- Stage into a temp/staging table and atomically swap or MERGE into the target — never let consumers read half-loaded tables.
- Make backfills a first-class parameterized path (same code, explicit date-range parameter), not a hand-edited copy of the DAG; test that backfilled and incremental outputs match.
- Track per-run metadata (rows extracted/loaded/rejected, watermark, duration) in an audit table; row-count deltas versus source are your cheapest correctness check.
- Prefer extracting from replicas, log-based CDC, or vendor bulk-export APIs over hammering production OLTP with SELECT *; rate-limit and schedule around source load.

## Pitfalls
- Non-idempotent inserts plus orchestrator retries = duplicated rows discovered weeks later in revenue dashboards.
- Timezone and DST bugs in watermark logic — always store and compare UTC, and beware sources emitting local time without offset.
- Transforming during extraction ("just a little cleanup in the extract query") so raw data is unrecoverable when the cleanup logic turns out wrong.

## Tools & references
Fivetran/Airbyte/Meltano (extract-load), dbt (transform), "Fundamentals of Data Engineering" (Reis & Housley), Maxime Beauchemin's "Functional Data Engineering" essay.
