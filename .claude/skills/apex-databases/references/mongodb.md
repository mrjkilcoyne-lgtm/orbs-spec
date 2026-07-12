# MongoDB

## Scope
NoSQL document database (BSON format, schema-flexible). Clustering (sharding, replication), transactions (ACID in 4.0+), aggregation framework, and operational considerations.

## Core principles
- Documents are self-contained JSON-like objects (BSON). Schema is flexible but not schemaless; your app enforces structure. Migration means writing code to reshape documents, not running ALTER TABLE.
- Sharding (distributing documents across multiple servers by a shard key) is built-in. The shard key determines which server stores each document; choose it to avoid hot shards (one server getting all writes) and to match your access patterns.
- Replication sets (primary + secondaries) provide redundancy and enable reads from secondaries. Writes go to the primary; secondaries lag behind due to async replication. Read preferences control this: primaryOnly, secondaryPreferred, etc.
- Transactions (ACID starting in 4.0) require replication sets; they span multiple documents and rollback fully on failure. Transactions are slower than eventual-consistency operations, so use them judiciously (financial transfers, not every operation).
- Indexes (similar to SQL databases) speed up queries. MongoDB scans one index, not multiple; the query planner chooses the "best" index. Compound indexes support multi-field queries and sorting.

## Apex practices
- Design collections and shard keys with access patterns in mind: if you often query by user_id, consider sharding by user_id. Avoid shard keys with low cardinality (status: pending/complete) to prevent hot shards.
- Use aggregation pipelines (MATCH, GROUP, SORT, PROJECT) for complex queries; they're more expressive and performant than multiple query calls. Pipeline stages operate in sequence; early MATCH stages reduce data volume.
- Embed related data (arrays of subdocuments) if the array is small and accessed together. Link via ObjectId for large or separate collections. This balances query simplicity vs update efficiency.
- Monitor oplog (the operations log used for replication); a secondary can only catch up if its lag is smaller than oplog size. Set oplog size appropriately for your write rate.

## Pitfalls
- Choosing a bad shard key (low cardinality, sequential, monotonically increasing) leading to hot shards and uneven data distribution.
- Embedding large or unbounded arrays (e.g., all comments on a post) in a document; arrays that grow without limit cause document growth and eventual 16MB limit violations.
- Assuming MongoDB is schema-free; in reality, your app has an implicit schema. Null checks and type coercion scatter through code if you don't define structure.

## Tools & references
MongoDB documentation (sharding, replication, transactions), MongoDB Atlas (managed service), Compass (GUI), "MongoDB: The Definitive Guide" (Chodorow), aggregation framework docs.
