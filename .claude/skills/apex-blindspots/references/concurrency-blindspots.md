# Concurrency Blindspots

## Scope
The races that survive review: check-then-act gaps, double execution, ordering assumptions — as a *blindspot pattern* across systems, not just threads.

## Core principles
- Check-then-act is the universal race shape: "if not exists, create," "if balance sufficient, deduct," "if file absent, write" — any gap between reading and acting invites an interleaving writer; the fix is making check-and-act one atomic operation (unique constraint, conditional write, compare-and-swap), never a faster check.
- Reviews miss races because reviewers execute code single-threaded in their heads: the bug isn't on any line — it's between the lines, in an interleaving; you must ask "what if two of these run at once?" explicitly, because nothing on the page will ask it for you.
- Everything user-facing runs concurrently already: double-clicked submit buttons, two open tabs, retried webhooks, replayed queue messages — you have a distributed concurrency problem even if your code has no threads.
- "It passed the test" means nothing for races: they're probabilistic, load-dependent, and timing-shifted by the act of observing (adding logs reschedules threads) — absence of failures under light concurrency is absence of evidence.
- Shared mutable state is guilty until proven innocent: module-level caches, class variables, singletons with state, connection reuse — in concurrent servers each is a race unless explicitly synchronized or immutable.

## Detection tests
- For each check-then-act: what happens if the world changes between the check and the act?
- What does this endpoint/handler do when called twice concurrently with the same input? (Run it, don't reason it.)
- Which state here is shared across requests/tasks, and what protects it?

## Countermeasures
- Push atomicity to the storage layer: unique constraints, conditional updates (WHERE version = ?), UPSERT, transactions with the right isolation — the database's atomic primitives beat application-level locks you'll forget somewhere.
- Test concurrency deliberately: fire N parallel duplicates at every mutation in CI; race detectors (Go -race, TSan) where the language has them.
- Design for idempotency and commutativity first — operations safe to repeat and reorder shrink the interleaving space you must reason about.

## Tools & references
Race detectors (TSan, Go -race), Jepsen's mindset applied small, "check-then-act" literature, database isolation-level docs.
