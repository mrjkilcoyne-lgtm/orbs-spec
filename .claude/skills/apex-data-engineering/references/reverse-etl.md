# Reverse ETL

## Scope
Syncing derived analytical data from the warehouse back to operational systems (CRM, marketing platforms, product DBs). Ensuring durable identity, eventual consistency, and correctness under failures.

## Core principles
- Reverse ETL is a data-sync problem wearing a business label: you're extracting from the warehouse as the source, transforming/enriching rows, and loading into operational destinations. Standard sync patterns (upsert by key, idempotency, dedup) apply — but now destinations are external APIs with rate limits and flaky semantics.
- Durable identity across systems is the foundation: map warehouse entity keys (customer_id, account_id) to destination IDs (Salesforce lead ID, Segment user ID, Klaviyo email) once, cache them reliably, and version the mappings. Key mismatches silently corrupt downstream CRM state.
- Eventual consistency and partial failures are the model: a sync run may update some API targets and fail on others. Track per-destination offset/cursor (which batch was last successfully synced), so retries resume from the failure point, not the beginning. Accept that operational systems lag the warehouse by minutes to hours.
- Segment destinations into cohorts deterministically: if a warehouse query puts the same customer into "email_nurture" AND "email_suppress" in different runs, downstream systems will thrash. Materialized segments with explicit priority rules (suppress beats nurture) make this debuggable.
- Handle schema drift and late-binding carefully: operational destinations change schemas (Salesforce adds/removes custom fields, Segment nixes old properties) without notice. Gracefully skip unmappable columns; log unmappable rows to a quarantine table for manual review, don't crash.

## Apex practices
- Build the sync as a warehouse query → parquet staging table → parameterized destination-loader code, with the intermediate table persisted for auditing and replay. If the API call fails halfway through a batch, you can resume from the staging table without re-querying the warehouse.
- Implement destination-side dedup windows: accept a grace period (24h typical) where duplicate API payloads are idempotent. Most destinations (Salesforce, HubSpot) support upsert by external ID, so send the same batch twice and get the same result.
- Track sync metadata per destination-batch: rows touched, bytes sent, API call latency percentiles, and row-level error logs (bad email, rate-limited, schema mismatch). Use this to measure freshness SLAs and prioritize fixes.
- Implement fan-out as separate runs per destination, not a fanout inside one Airflow task. Destination failures (API outage, quota exceeded) are independent; one broken API shouldn't block syncs to others. Orchestrate as a parallel task graph.

## Pitfalls
- Syncing without immutable source identity: using email or name as the destination key, then silently updating the wrong customer when email changes in the warehouse.
- Non-idempotent destination updates without dedup windows: crashing on a retry results in two email sends, two Stripe webhook calls, or two Salesforce lead creations for one customer.
- Ignoring schema mismatch: mapping every warehouse column to a destination property, so any add/drop/rename cascades and breaks; instead, explicitly map (whitelist) and skip unknown columns.

## Tools & references
Fivetran, Census, Hightouch, Meltano tap-to-target (reverse), "Fundamentals of Data Engineering" (Reis & Housley) — reverse ETL chapter, idempotency patterns from IETF drafts.
