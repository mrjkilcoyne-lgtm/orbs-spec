# Backup & Recovery

## Scope
Protecting data against loss through backups. RPO (recovery point objective), RTO (recovery time objective), point-in-time recovery (PITR), and testing backup-restore workflows.

## Core principles
- RPO is the maximum acceptable data loss (how fresh must backups be): 1 hour RPO means losing up to 1 hour of transactions is acceptable. RTO is the maximum acceptable downtime (how fast can you restore): 10 minute RTO means users are down max 10 minutes.
- Full backups capture the entire database; incremental backups capture only changes since the last backup. Full+incremental saves space but incremental restoration requires replaying multiple backups (slower, more complex).
- Point-in-time recovery (PITR) restores the database to any moment in the past using full backups + transaction logs (WAL in PostgreSQL, binlog in MySQL). Critical for undoing accidental deletes or schema mistakes; enables "restore to 2 minutes before disaster."
- Backups must be stored off-site (different cloud, different region) or on different physical hardware. A backup on the same disk as the database is useless if the hardware fails.
- Recovery procedures must be tested regularly: restore from backup, verify data integrity, measure restore time. Untested backups fail when you need them (Murphy's law).

## Apex practices
- Use managed backup services (AWS RDS backup, Google Cloud SQL backup) when available; they handle PITR, off-site storage, and encryption with minimal overhead.
- Schedule full backups during low-traffic windows (nightly) and incremental backups frequently (hourly). Calculate retention (3 months of daily backups, 1 year of weekly backups) based on compliance requirements.
- Implement backup monitoring: alert if backup fails, if backup size grows unexpectedly (sign of data corruption), if PITR window shrinks (transaction log pruning too aggressive).
- Automate restore testing: periodically restore a backup to a staging environment, run data-integrity checks, measure restore time. Catch backup failures before production disaster.

## Pitfalls
- Assuming replication is a backup (it's not): a replica shows real-time data but a logical error (delete all users) replicates immediately. Backups and replication serve different purposes.
- Not testing restore procedures until needed; discovering restore-time errors (backup corrupted, restore takes 12 hours when SLA is 1) during a disaster is catastrophic.
- Storing backups in the same region as the primary database; natural disaster (fire, flood) kills both.

## Tools & references
PostgreSQL pg_basebackup (full backup) and WAL archiving (PITR), MySQL mysqldump (logical backup) and binary logs, AWS RDS automated backups, pg_restore for PostgreSQL, backup verification tools (pg_filedump, MySQL recovery toolkit), "PostgreSQL High Availability" (Riggs & Bohn).
