# Stream Processing

## Scope
Continuous computation over unbounded data: event time vs processing time, windowing, watermarks, state, and exactly-once semantics in systems like Flink, Kafka Streams, and Spark Structured Streaming.

## Core principles
- Event time vs processing time is the foundational distinction (Akidau's Dataflow model): results keyed to when events happened require watermarks — a heuristic assertion that "no events older than T are still coming" — to know when windows can close.
- Correctness under out-of-order data is a triangle of completeness, latency, and cost: you can wait longer (higher latency), emit early and retract/update (more complexity), or drop late data (less complete) — choose explicitly per pipeline.
- "Exactly-once" means exactly-once state updates and effects within the system (checkpointed state + transactional/idempotent sinks), not exactly-once delivery — the network still delivers at-least-once; the sink must dedup or transact.
- Streaming state is a database you now operate: keyed state must be partitioned with the stream, checkpointed (Flink's Chandy-Lamport-style barriers), sized (RocksDB spill), and given TTLs before it grows without bound.
- Backpressure is a feature: a system that slows ingestion under load degrades gracefully; one that buffers unboundedly or drops silently fails catastrophically later.

## Apex practices
- Set allowed-lateness deliberately from measured event-delay distributions (p99 arrival skew), and route later-than-allowed events to a side output for audit rather than silently discarding.
- Use windows that match the question: tumbling for periodic aggregates, sliding for moving metrics, session windows (gap-based) for user activity — and prefer incremental aggregation over buffering raw events per window.
- Design sinks idempotent or transactional first (upsert by key, Kafka transactions, two-phase commit sinks); retrofitting exactly-once onto an append-only sink is a rewrite.
- Rehearse recovery: measure checkpoint size and restore time, and verify you can replay from the source (Kafka retention ≥ max outage + reprocessing window).

## Pitfalls
- Keying windows on processing time and shipping dashboards whose numbers change depending on lag and redeploys.
- Unbounded keyed state from high-cardinality keys with no TTL (e.g., per-session state for sessions that never "end").
- Assuming Kafka partition order equals global order — order holds only per partition per key; cross-key logic needs explicit reordering or event-time reasoning.

## Tools & references
Apache Flink, Kafka Streams, Spark Structured Streaming; "Streaming Systems" (Akidau, Chernyak, Lax) and the Dataflow paper (VLDB 2015); Flink's checkpointing docs.
