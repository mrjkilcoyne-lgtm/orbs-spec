# Distributed Consensus

## Scope
Agreement among unreliable nodes: Raft/Paxos, quorums, leader election, what consensus buys and costs.

## Core principles
- Consensus makes N machines act as one consistent state machine (replicated log) despite crashes and partitions — it's the foundation under etcd, Spanner, and every "just works" coordination service.
- FLP impossibility: no deterministic consensus in fully async systems; practical protocols buy progress with timeouts (partial synchrony) — safety never depends on timing, only liveness.
- Quorum intersection is the trick: any two majorities overlap, so a new leader always sees committed entries; f failures tolerated needs 2f+1 nodes.
- Leadership is a lease, not a fact: a deposed leader may not know it — fencing tokens, not "I think I'm leader," protect external effects.
- Consensus is expensive (round trips, majority availability): use it for metadata/coordination/config, not the data hot path; most systems need less consistency than they reach for.

## Apex practices
- Don't build it: use Raft libraries or delegate to etcd/ZooKeeper/cloud primitives; original consensus code is a research project.
- Odd cluster sizes (3 or 5); more nodes slow writes without adding fault tolerance beyond the quorum math.
- Place replicas across failure domains that match the quorum math (3 AZs for 3 nodes) — two nodes in one AZ is one failure from unavailability.
- Monitor leader elections and commit latency; election storms signal network/timeout misconfiguration.

## Pitfalls
- Distributed locks without fencing: the paused-process-wakes-up-and-writes bug (Kleppmann's Redlock critique).
- Even-sized clusters (4 nodes = 3-node fault tolerance at 4-node cost).
- Reading from followers and assuming linearizability.

## Tools & references
Raft paper (Ongaro) + thesecretlivesofdata.com, "Designing Data-Intensive Applications" ch. 8-9, etcd/ZooKeeper docs.
