# Message Queues & Brokers

## Scope
Asynchronous messaging infrastructure: queue vs log semantics, delivery guarantees, operational patterns.

## Core principles
- Two families: queues (SQS/Rabbit — message consumed and gone, competing consumers) vs logs (Kafka — retained, replayable, consumer groups track offsets). Choose by whether history and replay matter.
- Delivery guarantees are three-body problems: at-most-once, at-least-once (the practical default), exactly-once (requires idempotency or transactions end-to-end).
- Acknowledgment discipline defines correctness: ack after processing, not on receipt; visibility timeouts must exceed worst-case processing time.
- Backpressure is a feature: bounded queues with explicit overflow policy beat unbounded queues that hide overload until OOM.
- Poison messages need a plan: max receive count → DLQ → alert → replay tooling, or one bad message halts a partition forever.

## Apex practices
- Make consumers idempotent (dedup keys, conditional writes) — this single property forgives most delivery-semantics sins.
- Monitor queue depth and consumer lag as first-class SLIs; growing lag is the earliest overload signal.
- Size partitions/concurrency around ordering needs: key by entity when its events must serialize, maximize parallelism otherwise.
- Test consumer crash mid-processing: the redelivery path is the correctness path.

## Pitfalls
- Long-running work under a short visibility timeout (silent duplicate processing).
- Using the queue as a database (querying, random access, infinite retention on a queue-family broker).
- One consumer group reading a topic for two unrelated purposes (coupled scaling and offsets).

## Tools & references
Kafka/RabbitMQ/SQS/NATS docs, "Kafka: The Definitive Guide," enterprise integration patterns (Hohpe).
