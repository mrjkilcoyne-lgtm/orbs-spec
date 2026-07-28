# Kotlin

## Scope
Kotlin for JVM/Android/multiplatform: null safety, coroutines, expressive DSLs.

## Core principles
- Nullability in the type system is the headline feature; `!!` reintroduces the NPE you paid to remove.
- Data classes + sealed hierarchies + `when` exhaustiveness = domain modeling with compiler enforcement.
- Coroutines are structured concurrency: children live inside a scope, cancellation flows down, failures flow up.
- Extension functions add API without inheritance; use for domain vocabulary, not to monkey-patch everything.
- Prefer expressions (if/when as values, single-expression functions) — Kotlin's grain is expression-oriented.

## Apex practices
- `suspend` functions for async, Flow for streams; never block inside coroutines (Dispatchers.IO for legacy blocking).
- Scope functions (`let`, `apply`, `run`) sparingly and consistently — overuse creates puzzle code.
- Immutable `val` + persistent collections by default; expose read-only interfaces (List, not MutableList).
- Use `Result`/sealed results at boundaries rather than exception control flow.

## Pitfalls
- GlobalScope launches that outlive their logical owner (leaks, crashes after teardown).
- Platform types (Java interop) silently nullable — annotate Java or assert at the boundary.
- Overloading operators/DSLs until code is unreadable to newcomers.

## Tools & references
Kotlin docs, kotlinx.coroutines guide, detekt, ktlint; "Kotlin in Action."
