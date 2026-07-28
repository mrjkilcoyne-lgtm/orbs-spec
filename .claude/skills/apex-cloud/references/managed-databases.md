# Managed Databases

## Scope
Cloud-native data stores: RDS, Cloud SQL, Cosmos DB, DynamoDB, Firestore; trade-offs between managed and self-hosted.

## Core principles
- Managed databases handle replication, backups, and failover — you pay for convenience but lose some control.
- Consistency models differ (strong, eventual, transactional); choose based on your query patterns, not by default.
- Scaling databases is different from scaling compute: read replicas are easy, sharding is hard, backup/restore times scale with data size.
- Backup strategy must be explicit: frequency, retention, recovery time (RTOs), point-in-time recovery — test restores.
- Connectivity to managed databases from applications requires access management (security groups, database users, encryption in transit).

## Apex practices
- Use read replicas for read-heavy workloads (analytics, reporting) to offload queries; write replicas (multiple primaries) require conflict resolution.
- Implement point-in-time recovery (PITR) for all production databases — enable binary logging and automate backup validation.
- Use database activity monitoring and audit logging (query logs, DDL changes) for compliance and debugging.
- Choose instance types carefully: memory-optimized for in-memory databases, compute-optimized for complex queries, small instances for low-traffic databases.

## Pitfalls
- Managed databases as cheap as self-hosted (they're not — you're paying for operational simplicity; this is a feature, not a bug).
- Single-AZ database (if the AZ fails, you lose the database) — always multi-AZ or multi-region for critical data.
- No backups or backups in the same region (regional disaster loses everything) — replicate backups to another region.

## Tools & references
AWS RDS, GCP Cloud SQL, Azure Database, DynamoDB for NoSQL, Firestore for document storage, MongoDB Atlas for managed MongoDB, Terraform provider documentation.
