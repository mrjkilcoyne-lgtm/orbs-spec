# Change Data Capture

## Scope
Streaming database changes to downstream systems: log-based CDC (Debezium et al.), snapshot + stream coordination, ordering, and building correct replicas from change events.

## Core principles
- Log-based CDC (reading the WAL/binlog/oplog) is the only approach that captures every change including deletes, adds near-zero source load, and preserves transaction order — query-based polling ("rows where updated_at > X") misses deletes, intermediate states, and hard-deletes rows silently.
- CDC is snapshot + stream: a consistent initial snapshot must be coordinated with the log position where streaming begins (Debezium does this with watermark-based incremental snapshots) or you get gaps or duplicates at the seam.
- Delivery is at-least-once; consumers see duplicates on connector restarts. Correct downstream state requires idempotent apply — upsert by primary key with ordering protection (LSN/GTID comparison), never blind inserts.
- Ordering is per-key at best: events for one primary key must land in one Kafka partition (key by PK); cross-table transactional atomicity is lost by default unless you consume Debezium's transaction metadata topics and buffer.
- The replication slot is a loaded gun pointed at the source: an unconsumed Postgres slot pins WAL and can fill the source's disk; slot lag monitoring is production-critical, not optional.

## Apex practices
- Emit to a schema-registry-governed topic per table with the Debezium envelope (before/after/op/ts/source LSN), and keep tombstones enabled if you rely on compacted topics for latest-state.
- Handle schema changes end-to-end before you need to: test ADD COLUMN, type widening, and table renames through the whole path (connector → registry compatibility mode → consumer), because sources will change without asking.
- Materialize replicas with merge logic that applies inserts/updates/deletes by PK and discards out-of-order events by comparing source position — and validate periodically with row-count and checksum comparisons against the source.
- Plan the re-snapshot path (incremental snapshots, signal tables) for when a topic is corrupted or a new consumer needs full history — "we'd have to re-snapshot" should be a runbook, not a crisis.

## Pitfalls
- Confusing CDC events with domain events: a raw row-change stream leaks schema internals to every consumer; wrap or transform (outbox pattern) before it becomes a public contract.
- Forgetting REPLICA IDENTITY FULL / supplemental logging, so update/delete events lack before-images and downstream merge logic can't work.
- Snapshotting a large table through the connector during peak hours, holding long transactions and starving the source — schedule and throttle initial loads deliberately.

## Tools & references
Debezium docs (the reference implementation), Postgres logical decoding / MySQL binlog / Mongo change streams, Kafka Connect, the outbox pattern (Debezium outbox SMT), DBLog paper (Netflix) for incremental snapshots.
