# Event-Driven Architecture

## Scope
Systems communicating through events: pub/sub topologies, event design, sourcing, choreography vs orchestration.

## Core principles
- Events are facts, not commands: "OrderPlaced" (happened, immutable) vs "PlaceOrder" (please do) — mixing them tangles ownership.
- Producers don't know consumers: the decoupling is the point, and the cost is traceability — invest in correlation IDs and tracing upfront.
- Delivery is at-least-once in practice: consumers must be idempotent; exactly-once is a system property you build, not a broker checkbox.
- Ordering exists only within a partition/key: design keys around the entities whose event order matters.
- The event schema is a public API: version it, evolve additively, use a schema registry — a renamed field breaks consumers you've never met.

## Apex practices
- Choreography for loose coupling between domains; orchestration (explicit workflow) when a business process needs visibility, timeout handling, and compensation — most systems need both.
- Outbox pattern to publish events atomically with state changes; dual-write (DB then publish) loses events on crash.
- Dead-letter queues with alerting and replay tooling; a DLQ nobody drains is silent data loss.
- Document event flows (who emits, who consumes, why) — the architecture is invisible in any one repo.

## Pitfalls
- Event chains implementing what's really a synchronous workflow, with no visibility into where it stalled.
- Fat events carrying full entities (consumers couple to everything) vs anemic events forcing callbacks — design payloads deliberately.
- Assuming order across partitions or topics.

## Tools & references
Kafka/Pulsar/NATS docs, "Designing Event-Driven Systems" (Stopford), schema registries, Temporal for orchestration.
