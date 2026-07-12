# Distributed Transactions & Sagas

## Scope
Multi-step operations across services/stores: sagas, compensation, outbox, workflow engines.

## Core principles
- Cross-service ACID doesn't exist in practice: 2PC blocks on coordinator failure and couples availability; the mainstream answer is sagas — a sequence of local transactions with compensations.
- Compensation is not rollback: it's a new forward action (refund, release hold) that must itself handle failure; some steps are non-compensatable (sent email) — order them last.
- Every saga step must be idempotent and every trigger deliverable at-least-once; the saga pattern collapses without both.
- Choreography (events trigger next steps) scales loosely but hides the process; orchestration (a coordinator drives) centralizes visibility, timeouts, and compensation logic — prefer orchestration once the flow has >3 steps or needs monitoring.
- The outbox pattern is the atomicity primitive: write state change + outgoing message in one local transaction; a relay publishes — this closes the dual-write hole everything else leaks through.

## Apex practices
- Design the failure matrix before coding: for each step — retry? compensate? park for human? The matrix is the saga.
- Use a workflow engine (Temporal & co.) for non-trivial sagas: durable state, retries, timers, and visibility are exactly what they productize.
- Distinguish business failure (insufficient funds → compensate) from technical failure (timeout → retry); conflating them refunds customers because a network blipped.
- Emit saga state transitions as events for observability; "where is order 12345 stuck" must be answerable in one query.

## Pitfalls
- Semantic lock leakage: reserved inventory never released because compensation wasn't wired to every failure path.
- Assuming compensations succeed (they need retries and DLQs too).
- Rebuilding a workflow engine ad hoc via cron jobs, status columns, and hope.

## Tools & references
Garcia-Molina saga paper, Temporal docs, outbox/Debezium, "Microservices Patterns" (Richardson).
