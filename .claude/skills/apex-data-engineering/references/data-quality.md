# Data Quality

## Scope
Detecting, preventing, and managing bad data: validation checks, anomaly detection on data, quality dimensions, and the circuit-breaker vs warn decision.

## Core principles
- Quality is multidimensional — completeness, accuracy, consistency, timeliness, validity, uniqueness — and each needs its own check type; "the pipeline succeeded" measures none of them.
- Check placement is a blast-radius decision: validate at ingestion (quarantine bad rows early, cheap to fix), at transformation boundaries (catch logic bugs), and at publication (protect consumers) — the later a bad record is caught, the more downstream state must be repaired.
- Distinguish hard checks (schema, primary-key uniqueness, referential integrity, not-null on keys) that should stop the pipeline, from soft checks (volume drift, distribution shift, freshness) that should alert — stopping on every statistical wobble trains everyone to ignore the red.
- Expectations must be versioned, code-reviewed artifacts colocated with the pipeline (dbt tests, Great Expectations suites), not tribal knowledge — a check nobody can find is a check nobody maintains.
- Most real incidents are silent semantic drift, not nulls: an upstream team changes an enum meaning, a currency, or a dedup rule. Volume/distribution monitors and data contracts with producers catch what row-level rules can't.

## Apex practices
- Start every table with the four baseline tests — unique key, not-null key, accepted values on enums, referential integrity to parents — then add distribution and freshness monitors on the business-critical columns only.
- Track row counts and key aggregates (revenue, event counts) against the source and against historical seasonality; a 30% day-over-day volume drop should page before a consumer notices.
- Route failed rows to quarantine/dead-letter tables with rejection reasons and a reprocessing path — dropping them destroys evidence, and failing the whole load for 0.01% bad rows destroys freshness.
- Publish quality status to consumers (dashboards, table-level badges, or blocking freshness/quality checks in the BI layer) so "can I trust this table right now" has an answer other than Slack archaeology.

## Pitfalls
- Testing only structure, never meaning: schema is valid, keys are unique, and revenue is double-counted because a join fanned out.
- Alert fatigue from unactionable checks — hundreds of warnings per day guarantee the real incident scrolls by unread; every alert needs an owner and an action.
- Auto-coercing bad values (nulls to 0, bad dates to 1970-01-01) instead of rejecting them, turning detectable errors into plausible lies.

## Tools & references
dbt tests, Great Expectations, Soda, Monte Carlo/Bigeye (observability), Deequ (Spark); the data contracts literature (Chad Sanderson) and DAMA-DMBOK quality dimensions.
