# Apache Kafka

## Scope
Kafka as the durable event backbone: topics, partitions, consumer groups, delivery semantics, retention/compaction, and operating producers and consumers correctly.

## Core principles
- Kafka is a distributed, partitioned, replicated commit log — not a queue: consumers track their own offsets, messages aren't deleted on read, and multiple consumer groups read the same data independently at their own pace.
- Ordering is guaranteed only within a partition; the partition key is therefore a semantic decision (all events for one order/user in order) and a load-balancing decision (hot keys create hot partitions) at the same time.
- Delivery semantics live at the edges: at-least-once is the baseline; "exactly-once" requires idempotent producers (`enable.idempotence=true`), transactions for consume-transform-produce, and consumers that commit offsets atomically with side effects — or idempotent sinks.
- Partition count is a near-permanent choice: you can add partitions (breaking key→partition mapping for existing data) but never remove them; plan from target throughput ÷ per-partition throughput, plus headroom, because max consumer parallelism = partition count.
- Durability is `acks=all` + `min.insync.replicas=2` + replication factor 3; anything weaker trades away written-but-lost messages during leader failover — and unclean leader election must stay off for data you care about.

## Apex practices
- Monitor consumer lag (per group, per partition) as the primary health metric, alert on lag growth rate rather than absolute lag, and watch for rebalance storms — use cooperative-sticky assignment and static group membership to tame them.
- Put schemas on every topic via Schema Registry (Avro/Protobuf/JSON Schema) with a declared compatibility mode; a schemaless topic is an integration incident on a timer.
- Choose retention per topic deliberately: time/size-based deletion for event streams (retention ≥ longest realistic replay/outage window), log compaction for changelog/latest-state topics — and remember compaction keeps the latest value per key, not history.
- Handle poison messages explicitly: bounded retries, then a dead-letter topic with error metadata — a consumer that hot-loops on one bad record silently stops the whole partition.

## Pitfalls
- Committing offsets before processing completes (silent data loss on crash) or auto-commit with long processing (duplicates and lost work on rebalance).
- Keying by a low-cardinality or celebrity-skewed field, then wondering why one broker and one consumer run hot while the rest idle.
- Treating Kafka as a database or an RPC layer: request/response over topics, unbounded retention as "storage," or reading a topic to answer point queries.

## Tools & references
"Kafka: The Definitive Guide" (2nd ed.), Kleppmann's "Designing Data-Intensive Applications" ch. 11, Confluent Schema Registry docs, kcat/kafka-consumer-groups tooling, KIP-98 (exactly-once) design doc.
