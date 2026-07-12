# Cassandra

## Scope
Distributed NoSQL database (peer-to-peer, no single leader). Eventual consistency, tunable replication, and write-heavy time-series workloads. Apache Cassandra and managed services (DataStax, AWS).

## Core principles
- Cassandra is a write-optimized, distributed database: every node accepts writes, and data is replicated to multiple nodes asynchronously. No coordination overhead (no leader election like in consensus systems).
- Replication factor (RF) and consistency levels (CL) are tunable: RF=3 means each row is stored on 3 nodes; CL=QUORUM means the coordinator waits for 2 out of 3 responses before acknowledging. Higher CL trades off write latency for consistency guarantees.
- Data is partitioned by partition key (hash-based): rows with the same partition key are stored together (in a sorted order by clustering key). Query by partition key is fast; queries without it full-scan the cluster.
- Eventual consistency is the model: after a write, not all replicas have the data immediately. Read repair (background anti-entropy) converges replicas over time. Conflicts are resolved by last-write-wins (timestamp-based).
- Compaction merges and deduplicates SSTables (immutable sorted tables on disk). Different strategies (Leveled, Size-Tiered, Time-Windowed) tune the write-amplification vs read-latency tradeoff.

## Apex practices
- Design schema for your queries, not for normalization: in Cassandra, denormalization is the norm. One partition key per query pattern; use multiple tables (same data, different clustering keys) if you have different access patterns.
- Set RF=3 and CL=QUORUM for strong consistency where you need it; RF=2, CL=ONE for high-throughput eventual-consistency use cases (time-series, logs).
- Use TTL (time-to-live) liberally; rows expire automatically and are removed during compaction. Critical for time-series data (don't accumulate gigabytes of old metrics).
- Monitor commit log size and compaction progress; if compaction can't keep up with writes, the disk fills and the node dies. SSTables should stay balanced across disks.

## Pitfalls
- Designing schema with too many partitions or too few; too many partitions (one per write) prevents efficient reads; too few (all data in one partition) overloads a single node.
- Not setting RF and CL appropriately for your consistency needs; thinking "higher is always better" incurs latency penalties and doesn't give ACID.
- Ignoring compaction strategy; the default Size-Tiered is fragmented and causes read amplification. Leveled is better for read-heavy workloads.

## Tools & references
Cassandra documentation (read path, write path, compaction), DataStax drivers (Python, Java), "Cassandra: The Definitive Guide" (Hewitt), nodetool (admin CLI), visualizing replication topology.
