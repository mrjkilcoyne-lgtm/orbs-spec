# Java

## Scope
Modern Java (17+ LTS): records, sealed types, streams, the JVM.

## Core principles
- The JVM is the asset: JIT, GC choices, and observability maturity matter more than syntax.
- Immutability first: records for data, final fields, unmodifiable collections — mutation is the opt-in.
- Sealed interfaces + records + pattern matching give algebraic data types; use them for domain modeling.
- Checked exceptions at module boundaries are API design; don't laundering everything to RuntimeException without thought.
- Streams for transformation pipelines; loops for side effects and early exit — pick per readability.

## Apex practices
- Virtual threads (Loom) for IO-bound concurrency; structured concurrency for task trees.
- Dependency injection via constructor; keep frameworks (Spring) at the edges of the domain.
- JMH for benchmarks — naive timing lies on the JVM (warmup, JIT).
- Understand your GC (G1/ZGC) and heap sizing before "Java is slow" conclusions.

## Pitfalls
- `equals`/`hashCode` contract violations breaking collections silently (records fix this).
- Optional used as field/parameter type instead of return type.
- Stream pipelines with side effects that read as pure.

## Tools & references
Effective Java (Bloch), JMH, async-profiler, Spring/Quarkus, Error Prone.
