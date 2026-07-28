# Analytics Engineering (dbt)

## Scope
Transforming warehouse data with software-engineering discipline: dbt project structure, testing, incremental models, documentation, and the semantic layer.

## Core principles
- dbt's core contribution is bringing software practice to SQL: version control, code review, CI, tests, environments, and docs — the SQL was always possible; the discipline is the product.
- Layered project structure is the load-bearing convention: staging models (1:1 with sources, rename/cast/clean only) → intermediate (reusable business logic) → marts (consumer-facing facts/dims). Skipping staging couples every mart to raw-source quirks.
- Every model should have a declared materialization rationale: view (cheap, always fresh, pushes compute to query time), table (expensive queries read often), incremental (large facts where full rebuild is too slow/costly), ephemeral (inline CTE reuse) — defaulting everything to table is a cost decision made by accident.
- Incremental models are eventually wrong by design: late-arriving data and logic changes drift them from the full-refresh truth. Use lookback windows or merge on unique_key, and schedule/verify periodic full refreshes for reconciliation.
- Define metrics once: business logic duplicated across dashboards is how two executives get two revenue numbers — push shared logic down into marts or a semantic layer (MetricFlow, dbt metrics) with tested, documented definitions.

## Apex practices
- Enforce the minimum test floor in CI — unique + not_null on every model's primary key, accepted_values on enums, relationships to parents — and use `dbt build` (run + test in DAG order) so a failing test stops downstream models.
- Run slim CI on pull requests: `dbt build --select state:modified+ --defer` builds only changed models and their descendants against production artifacts, keeping PR feedback minutes-fast on thousand-model projects.
- Use sources with freshness checks (`dbt source freshness`) as the pipeline's front door, and exposures to declare dashboards/ML consumers so lineage reaches the artifacts people see.
- Treat ref() discipline as non-negotiable: no hardcoded table names inside models ever — ref/source are what make environments, lineage, and slim CI work.

## Pitfalls
- The 4,000-line model with 25 CTEs nobody can review — decompose into intermediate models; each model should answer one question and be testable alone.
- Incremental models with `is_incremental()` filters on updated_at but no unique_key merge or lookback, silently dropping late-arriving updates forever.
- dbt run in prod from laptops — without CI, state comparison, and scheduled jobs, you have artisanal SQL with extra YAML.

## Tools & references
dbt docs and "How we structure our dbt projects" (dbt Labs), MetricFlow/dbt Semantic Layer, sqlfluff for linting, elementary/dbt-artifacts for run observability.
