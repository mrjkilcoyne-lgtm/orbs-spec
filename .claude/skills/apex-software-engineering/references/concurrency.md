# Concurrency

## Scope
Correct and efficient programs with multiple threads of execution: shared memory, message passing, async.

## Core principles
- Shared mutable state is the enemy; prefer immutability, message passing, or single-writer designs.
- A data race is undefined behavior, not "occasionally wrong" — all shared access needs synchronization or ordering.
- Lock ordering must be global and documented to prevent deadlock.
- Async/await is cooperative: blocking in an async context starves the scheduler.
- Concurrency (structure) and parallelism (execution) are different goals; design for the one you need.

## Apex practices
- Confine state: own data in one goroutine/actor/thread and communicate via channels/queues.
- Make cancellation first-class (contexts, tokens) and propagate it through every blocking call.
- Bound everything: pools, queues, in-flight requests — unbounded concurrency is a self-DoS.
- Use race detectors and stress tests in CI, not just on repro.

## Pitfalls
- Sprinkling locks until it "works" — check-then-act races survive coarse locking.
- Fire-and-forget tasks whose panics/exceptions vanish.
- Assuming ordering across threads without a happens-before edge.

## Tools & references
Go race detector, ThreadSanitizer, java.util.concurrent, structured concurrency (Trio, Kotlin, Java Loom).
