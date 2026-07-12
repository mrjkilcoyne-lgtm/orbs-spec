# Data Lineage

## Scope
Tracking where data comes from and where it flows: table/column-level lineage, impact analysis, root-cause debugging, and lineage capture mechanisms.

## Core principles
- Lineage answers two directional questions: upstream ("this dashboard is wrong — which sources feed it?") for root cause, and downstream ("we're changing this column — who breaks?") for impact analysis. A lineage system that can't answer both quickly isn't earning its keep.
- Granularity determines usefulness: table-level lineage says *that* systems connect; column-level lineage says *what* actually depends on what — and most breaking changes are column-level (renames, type changes, semantic drift).
- Automatically captured lineage beats documented lineage, always: parse it from SQL (dbt's manifest, warehouse query logs, SQL parsers like sqlglot) or emit it from runtime (OpenLineage events) — hand-maintained lineage diagrams are wrong within a month.
- Lineage has blind spots at system boundaries: spreadsheets, notebooks, reverse-ETL syncs, and application code that reads the warehouse are where lineage graphs go dark — and where incidents love to originate.
- Lineage is metadata with a freshness SLA of its own: stale lineage confidently pointing at removed tables is worse than no lineage; capture must run with every deployment/execution, not as a quarterly crawl.

## Apex practices
- Standardize on OpenLineage-compatible emission across orchestrators (Airflow, Dagster, Spark integrations) so lineage from heterogeneous systems lands in one graph (Marquez, DataHub, warehouse-native lineage).
- Wire lineage into the change workflow: CI on a dbt model change lists affected downstream models, exposures, and dashboard owners before merge — impact analysis as a merge gate, not a post-incident activity.
- Declare terminal consumers explicitly (dbt exposures, dashboard registrations) so the graph reaches the things executives actually look at, not just the last table.
- During incidents, walk lineage upstream from the broken artifact and cross-reference run metadata (which loads ran, when, with what row counts) — lineage plus run history is the root-cause toolkit.

## Pitfalls
- Buying a catalog with lineage and never integrating the long tail of pipelines, leaving a graph that covers 60% of flows — teams learn they can't trust it and revert to tribal knowledge.
- Treating lineage as read-only documentation instead of an operational input for CI checks, deprecation workflows, and incident tooling.
- Ignoring transformation semantics: lineage shows the edge but not that the join is a LEFT JOIN with a filter that drops 40% of rows — pair lineage with the actual SQL, not just arrows.

## Tools & references
OpenLineage spec + Marquez, DataHub, dbt docs/manifest lineage, warehouse-native lineage (Snowflake ACCESS_HISTORY, BigQuery lineage API), sqlglot/sqllineage for SQL parsing.
