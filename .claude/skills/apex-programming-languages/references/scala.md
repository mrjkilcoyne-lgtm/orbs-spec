# Scala

## Scope
Scala 3 on the JVM: fusion of OO and FP, the type system, effect ecosystems.

## Core principles
- Immutability + case classes + sealed traits + pattern matching = the default modeling toolkit.
- Expressions everywhere: `val` result of if/match; side effects are pushed to the edges.
- The type system rewards investment (givens/using, opaque types, union types) and punishes showing off.
- Pick a lane: vanilla-Scala-as-better-Java, cats-effect/ZIO pure FP, or Akka/Pekko actors — mixing paradigms per-file wrecks teams.
- Collections API is the daily driver: know map/flatMap/fold/groupBy and their laziness (views, iterators).

## Apex practices
- For-comprehensions as monadic sequencing (Option/Either/Future/IO) — the readable spine of Scala code.
- Model errors with Either/Validated over exceptions; reserve throwing for truly exceptional.
- Keep implicits/givens few, well-named, and in predictable locations (companion objects).
- Enforce style and complexity with scalafmt/scalafix; compile warnings as errors.

## Pitfalls
- Future without proper ExecutionContext discipline (blocking on the global pool).
- Implicit conversion magic nobody can trace.
- Library ecosystem splits (Scala 2 vs 3, cats vs zio) causing dependency deadlock — check compatibility first.

## Tools & references
Scala 3 book, cats/cats-effect or ZIO docs, scalafmt, "Programming in Scala" (Odersky).
