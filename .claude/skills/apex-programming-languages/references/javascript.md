# JavaScript

## Scope
Modern JavaScript (ES2020+) in browser and Node: the event loop, closures, and the ecosystem.

## Core principles
- Single-threaded event loop: everything blocks everything; long synchronous work freezes the UI/server.
- Microtasks (promises) run before macrotasks (timers) — ordering bugs live here.
- `this` is call-site-bound; arrow functions capture lexically. Most `this` bugs are one of these two rules.
- Coercion rules are unintuitive; use `===`, and treat truthiness checks on possibly-0/'' values as suspect.
- Modules are the unit of encapsulation; closures are the unit of private state.

## Apex practices
- async/await with real error handling; every floating promise is an unhandled rejection waiting.
- Prefer `const`, immutable updates (spread/`toSorted`), and small pure functions — the ecosystem's testable style.
- Know the platform APIs (fetch, URL, AbortController, streams) before reaching for packages.
- Use `Promise.all`/`allSettled` for independent async work instead of sequential awaits.

## Pitfalls
- `parseInt` without radix, `sort()` without comparator (lexicographic numbers).
- Mutating shared objects/arrays passed by reference across module boundaries.
- Relying on object key iteration order semantics you haven't verified.

## Tools & references
MDN, Node.js docs, ESLint, Vitest/Jest; "You Don't Know JS Yet" series.
