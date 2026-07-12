# Sharding

## Scope
Distributing data across multiple database instances by partition key. Consistent hashing, hotspot detection, and resharding strategies. Horizontal scaling beyond single-server limits.

## Core principles
- Sharding partitions data: shard key (e.g., user_id, account_id) determines which shard stores each row. Queries on the shard key are local (one shard); queries without it require fan-out to all shards (slow).
- Choose shard keys carefully: high cardinality (millions of unique values) prevents hotspots, good distribution across shards. Low cardinality (e.g., status: active/inactive) concentrates data on few shards, creating hotspots.
- Consistent hashing (or hash-ring) maps keys to shards smoothly: adding a shard rebalances only ~1/N data, not everything. Naive modulo hashing requires rebalancing the entire dataset on shard count changes.
- Resharding (migrating data when adding shards) is expensive: while resharding, some queries may hit multiple shards (old and new), creating complexity. Plan resharding carefully or use automatic systems.
- Cross-shard joins and transactions are hard: a join spanning two shards requires coordination (coordinator queries both, merges results). Distributed transactions use consensus (Raft, 2-phase commit) and are slow. Design schemas to avoid cross-shard queries.

## Apex practices
- Shard by natural domain entity (user_id, tenant_id, organization_id), not by hash of email or name. Business logic is tied to entities; sharding by entity simplifies query logic.
- Implement automatic shard discovery (service mesh, configuration server) so the application doesn't hardcode shard locations. Shard topology changes without downtime.
- Use consistent hashing so adding shards doesn't require full resharding; 1/N data moves to new shards, the rest stay put.
- Implement shard-aware connection pooling and query routing (middleware layer) to route requests to the correct shard and handle shard failures gracefully.

## Pitfalls
- Choosing a bad shard key with uneven distribution (e.g., user country, gender) leading to hotspots where one shard stores 90% of data.
- Resharding without proper tooling; manual data migration is error-prone and doesn't handle concurrent writes cleanly.
- Requiring cross-shard queries for common operations (filter users across all shards by status); consider denormalization or secondary indexes.

## Tools & references
Consistent hashing algorithm (Karger et al.), CockroachDB (automatic resharding), Citus/PostgreSQL (sharding extension), "Designing Data-Intensive Applications" (scaling chapter), shard-aware middleware (HyperLogLog for cardinality estimation).
