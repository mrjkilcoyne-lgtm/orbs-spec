# Disaster Recovery & Business Continuity

## Scope
Planning for and testing recovery from infrastructure failures: RTO, RPO, backup strategies, and failover.

## Core principles
- RTO (Recovery Time Objective, how fast you need to recover) and RPO (Recovery Point Objective, how much data you can afford to lose) are business decisions, not technical ones.
- Backup without restore testing is fiction — untested backups always fail when needed; test monthly.
- Multi-region replication is the only way to achieve sub-hour RTO; single-region backups have hours of recovery time.
- Failover is not automatic; you must plan detection (monitoring), decision-making (who decides to fail over?), and execution (how long does it take?).
- Documentation must be current; runbooks written during the last incident are outdated by the next one.

## Apex practices
- Implement automated backup and replication with retention policies; test restore at least monthly.
- Use active-active (both regions serving traffic) rather than active-passive (standby idle) to catch cross-region issues early.
- Run disaster recovery drills quarterly; rotate who participates so everyone learns.
- Implement health checks and automated failover for infrastructure (DNS failover, load balancer failover) to reduce manual steps.

## Pitfalls
- Backup retention too short (you discover data loss after backup rotation) — retain for long enough to detect corruption.
- Backup and primary in the same region (regional disaster loses everything) — replicate to another region or cloud.
- No runbook or untested runbooks (incident starts, operators improvise) — document and test every recovery procedure.

## Tools & references
AWS Backup, GCP Backup and DR, Azure Site Recovery, AWS DMS for database migration, database-specific replication (RDS, Cloud SQL), Terraform disaster recovery modules.
