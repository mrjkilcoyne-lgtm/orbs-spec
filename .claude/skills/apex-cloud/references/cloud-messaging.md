# Cloud Messaging & Event Streaming

## Scope
Asynchronous communication: message queues (SQS, Pub/Sub), event streaming (Kafka, Kinesis), and event sourcing patterns.

## Core principles
- Queues decouple producers from consumers — a producer publishes a message and returns; a consumer processes it asynchronously.
- Guarantees matter: at-most-once (fast, may lose messages), at-least-once (slow, may duplicate), exactly-once (complex, rare).
- Message retention (how long messages live in the queue) and visibility timeout (how long a consumer has to process) affect semantics.
- Ordering guarantees affect design: if order matters, use a single shard/partition; if you can tolerate out-of-order, scale horizontally.
- Dead-letter queues (messages that fail repeatedly) prevent stuck consumers and enable investigation.

## Apex practices
- Use message queues for background jobs (emails, notifications, data processing) — decouple from request path, scale consumer independently.
- Implement idempotent message handlers (messages may be delivered multiple times) using message IDs.
- Use pub/sub for broadcast events (many subscribers need to know about the same event) and queues for point-to-point.
- Implement exponential backoff with jitter for retries — avoid thundering herd when a service recovers.

## Pitfalls
- Using synchronous APIs instead of async (tight coupling, poor scalability) — queue the work, respond immediately.
- No dead-letter queue (messages that fail are lost or stuck) — implement DLQ to catch failures.
- Over-relying on ordering guarantees (single shard bottleneck) — design for out-of-order unless order is truly required.

## Tools & references
AWS SQS, SNS, Kinesis; GCP Pub/Sub; Azure Service Bus; Kafka for streaming; AMQP/MQTT protocols; "Enterprise Integration Patterns" by Hohpe & Woolf.
