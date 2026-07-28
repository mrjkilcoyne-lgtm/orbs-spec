# Transactions & Isolation

## Scope
ACID properties (Atomicity, Consistency, Isolation, Durability). Isolation levels (read uncommitted, read committed, repeatable read, serializable). Anomalies: dirty reads, non-repeatable reads, phantom reads.

## Core principles
- ACID is the contract: a transaction is all-or-nothing (atomic), moves the DB from one valid state to another (consistent), doesn't see other in-flight transactions (isolated), and once committed survives crashes (durable).
- Isolation levels are a spectrum: higher isolation (serializable) means less concurrency (locks), lower isolation (read uncommitted) means more concurrency but anomalies. The tradeoff is unavoidable.
- Dirty reads (reading uncommitted data): READ UNCOMMITTED allows this; higher levels prevent it. Most applications need at least READ COMMITTED to avoid correctness bugs.
- Non-repeatable reads (same query returns different results within a transaction): READ COMMITTED allows this; REPEATABLE READ prevents it by using consistent snapshots. Critical for balance-checking and inventory.
- Phantom reads (new rows appear between queries): REPEATABLE READ allows this (new rows inserted by others); SERIALIZABLE prevents it by holding range locks. Rare but possible in applications processing "all orders since yesterday."

## Core principles (continued)
- MVCC (Multiversion Concurrency Control) reduces locking: readers see a consistent snapshot, writers don't block readers. PostgreSQL uses MVCC; MySQL InnoDB also uses it. Traditional 2PL (two-phase locking) is simpler but slower.

## Apex practices
- Start with READ COMMITTED for OLTP systems; it prevents dirty reads (but not non-repeatable or phantom reads), covering most workloads. Escalate to REPEATABLE READ or SERIALIZABLE only where re-read consistency inside a transaction actually matters.
- Use explicit pessimistic locks (SELECT FOR UPDATE) only when you must ensure exclusive access (e.g., decrementing inventory by exactly 1). Optimistic locking (version columns) is often faster.
- Beware of implicit transactions in autocommit mode: a single statement is a transaction, but a series of statements without BEGIN/COMMIT are separate transactions. Wrap multi-statement operations in explicit transactions.
- Test anomalies: write tests that spawn concurrent transactions and verify the application handles phantom reads and non-repeatable reads correctly (e.g., balance doesn't go negative).

## Pitfalls
- Assuming a single query is transactional; it is, but a series of queries (read, compute, write) is only transactional if wrapped in BEGIN/COMMIT.
- Using lower isolation levels to "go faster" without understanding the anomalies; dirty data leads to silent bugs that are expensive to debug.
- Holding locks across network calls or external APIs; the lock contends with other transactions for the duration of the call, killing throughput.

## Tools & references
PostgreSQL documentation (isolation levels, MVCC), MySQL/InnoDB (isolation levels, locking), Jepsen's consistency testing framework, "Designing Data-Intensive Applications" (Kleppmann, chapter on transactions), anomaly examples.
