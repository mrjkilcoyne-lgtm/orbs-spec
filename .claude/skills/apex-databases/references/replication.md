# Replication

## Scope
Copying data across multiple database instances for redundancy and read scaling. Synchronous vs asynchronous replication, consistency models, and failover strategies.

## Core principles
- Primary-replica topology: primary accepts writes, replicas receive changes asynchronously and serve reads. Read scaling (horizontally add replicas) is the benefit; redundancy (failover if primary dies) is the safety net.
- Synchronous replication waits for replicas to acknowledge writes before committing; strong consistency but high latency (one slow replica slows everyone). Asynchronous replication acknowledges immediately; low latency but replicas may lag (stale reads possible).
- Replication lag is the norm in async systems: replicas lag seconds to minutes behind the primary. Application must handle eventual consistency (read-your-own-writes routing, eventual consistency caching).
- Consistency models: strong (all reads see the latest write), eventual (reads converge to the latest write over time), causal (writes that causally depend on each other are ordered). Each requires different implementation (synchronous replication, version vectors, etc.).
- Failover requires deciding which replica becomes the new primary. If the old primary is still alive, two primaries = split-brain = data divergence. Quorum (elect new primary if majority of replicas agree) or a consensus system (Raft, Paxos) prevents split-brain.

## Apex practices
- Use asynchronous replication for read scaling (load balance reads across replicas) and synchronous replication for specific high-value writes (financial transactions). PostgreSQL supports both.
- Monitor replication lag (how far behind replicas are) and alert if lag exceeds SLA. High lag means reads are stale; consider reducing write throughput or adding replicas.
- Implement read-your-own-writes: route writes to primary, then route subsequent reads from the same user to the primary (or wait for replication to catch up). Avoids user confusion.
- Test failover regularly (simulate primary crash, verify replicas detect it, elect new primary, application reconnects). Failover surprises break systems; run drills.

## Pitfalls
- Assuming async replication is transparent; replicas are eventually consistent, not immediately. Application must handle reads from replicas that may be stale.
- Not handling replica lag during failover; a replica elected as primary may not have the latest data from the old primary (data loss).
- Split-brain: two primaries accepting writes, data diverges, users get contradictory results. Requires quorum election or external arbiter to prevent.

## Tools & references
PostgreSQL replication (streaming, logical), MySQL replication (binlog-based, GTIDs), Raft consensus ("In Search of an Understandable Consensus Algorithm"), Jepsen consistency testing, "Designing Data-Intensive Applications" (chapters on replication).
