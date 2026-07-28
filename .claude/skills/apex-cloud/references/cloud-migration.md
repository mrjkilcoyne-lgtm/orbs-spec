# Cloud Migration

## Scope
Moving workloads from on-premises or other clouds to target cloud: planning, execution, cutover, and validation.

## Core principles
- Migration is not just moving VMs; it's an opportunity to rearchitect — lift-and-shift is faster but leaves legacy problems behind.
- The 6 R's (Rehost, Replatform, Refactor, Repurchase, Retire, Retain) define migration strategies; rehost is fastest, refactor is most beneficial.
- Cutover risk is managed by running parallel systems (old and new) until confidence is high; big-bang migrations are risky.
- Data migration is the slowest part (volume, validation, cutover coordination); plan for it early and test thoroughly.
- Post-migration optimization (stopping old systems, adjusting reserved instances, rightsizing) is often forgotten but provides the ROI.

## Apex practices
- Create a migration wave plan: group workloads by risk/criticality, migrate low-risk first (small databases, non-critical services), critical systems last.
- Implement automated validation (checksums, row counts, spot checks) to verify data integrity post-migration.
- Use AWS DMS, GCP Database Migration Service, or similar tools for zero-downtime database migrations where possible.
- Plan for rollback (if migration fails, what's the process to restore the old system?) — test it.

## Pitfalls
- Underestimating effort and timeline (always takes 2x longer than planned) — add buffer.
- No plan for dependencies (application A depends on B; migrate A first, now B doesn't work) — map dependencies before migration.
- Migration without validation (data looks correct but isn't) — implement automated checks before cutover.

## Tools & references
AWS Application Migration Service, AWS DMS, GCP Database Migration Service, Azure Database Migration Service, CloudEndure, Velostrata, "Cloud Migration Playbook" from cloud providers.
