# Orchestration (Airflow / Dagster)

## Scope
Scheduling and coordinating data pipelines as DAGs: dependency management, retries, backfills, data-aware scheduling, and the Airflow/Dagster/Prefect operating model.

## Core principles
- The orchestrator's job is dependency-correct, retry-safe, observable execution — not computation: tasks should push heavy work to Spark/warehouse/K8s and stay thin, or the scheduler becomes your least reliable compute cluster.
- Idempotent, parameterized tasks are the contract: every task run receives its logical/data interval (Airflow's `data_interval_start`, not `now()`) and can be re-run for any past interval to produce identical results — this is what makes backfills and retries safe.
- Schedule on data readiness, not wall clock, where possible: sensors, Airflow datasets, or Dagster's asset-based scheduling ("materialize when upstream assets update") eliminate the "upstream was late so everything downstream is wrong" class of failures.
- Dagster's core insight: model the assets (tables, files, models) as the first-class graph and derive tasks from them — you get lineage, freshness policies, and selective re-materialization that task-centric DAGs bolt on afterward.
- Retries only help transient failures: distinguish retryable (network, throttling) from deterministic failures (bad data, bugs) — retrying a deterministic failure 5 times with exponential backoff just delays the page by an hour.

## Apex practices
- Keep DAG files as declarative wiring: no heavy imports, API calls, or DB queries at module top-level (Airflow parses DAG files continuously); business logic lives in libraries tested independently of the orchestrator.
- Set SLAs/freshness policies and alert on data lateness, not just task failure — a pipeline that "succeeds" 6 hours late has still broken every downstream consumer.
- Design explicit backfill ergonomics: bounded concurrency (don't let a 2-year backfill starve daily runs), `depends_on_past` and catchup settings chosen deliberately, and idempotent writes so overlapping runs can't corrupt.
- Version and deploy pipelines like software: DAGs in git, CI that at minimum imports every DAG (catching syntax/import errors before the scheduler does), staged rollout, pinned dependency images per pipeline.

## Pitfalls
- Passing large data between tasks via XCom/inline results instead of external storage references — orchestrator metadata DBs are not data planes.
- `catchup=True` surprise: deploying a DAG with an old start_date and watching the scheduler launch hundreds of historical runs against production sources.
- Time-zone and schedule-semantics confusion: an Airflow run stamped `2024-01-01` processes the interval that *ends* then (data_interval semantics) — off-by-one-interval bugs from misreading this are endemic.

## Tools & references
Apache Airflow (TaskFlow API, datasets), Dagster (software-defined assets), Prefect, Temporal for workflow-as-code; "Data Pipelines with Apache Airflow" (Harenslak & de Ruiter).
