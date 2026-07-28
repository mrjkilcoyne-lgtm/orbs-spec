# Error Handling

## Scope
Designing how software detects, propagates, reports, and recovers from failures.

## Core principles
- Errors are part of the interface contract: enumerate what can fail and how callers should react.
- Distinguish expected failures (validation, not-found) from bugs (invariant violations); handle the first, crash loudly on the second.
- Handle errors at the level that has enough context to decide; propagate otherwise.
- Never swallow errors silently — log-and-continue is a decision, make it explicit.
- Error messages serve the person debugging at 3am: include what failed, with what inputs, and what to check.

## Apex practices
- Wrap errors with context at each boundary crossing (operation, identifiers) without duplicating stack traces.
- Design cleanup with the failure path in mind: defer/finally/RAII so partial failures don't leak resources.
- Test the error paths explicitly; they're the least-executed, highest-stakes code.
- Fail fast on startup misconfiguration rather than limping into runtime.

## Pitfalls
- Catch-all handlers that convert every failure into a generic 500 with no cause.
- Using exceptions for control flow of expected outcomes.
- Retrying non-idempotent operations on ambiguous failure.

## Tools & references
Language idioms (Go error wrapping, Rust Result, exception hierarchies), "Crash-only software" literature.
