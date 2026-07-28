# Design Patterns

## Scope
Recognizing recurring design problems and applying named solutions (GoF and beyond) without cargo-culting.

## Core principles
- Patterns are vocabulary for trade-offs, not goals; the problem must exist before the pattern applies.
- Prefer composition over inheritance; most classic patterns (Strategy, Decorator, Adapter) are composition shapes.
- Factories isolate construction knowledge; use them when creation logic varies, not by default.
- Observer/pub-sub decouples producers from consumers at the cost of traceability.
- In languages with first-class functions, many patterns collapse to passing a function.

## Apex practices
- Name the pattern in code only when it clarifies (e.g., `RetryStrategy`), never as noise (`FooManagerFactoryImpl`).
- Refactor toward a pattern when the third variant appears, not the first.
- Document the trade-off that justified the pattern next to its entry point.
- Know the inverse: when to inline a pattern away as requirements simplify.

## Pitfalls
- Speculative abstraction: applying patterns for imagined future needs.
- Singleton as global mutable state in disguise.
- Deep inheritance trees where Strategy/composition was the fit.

## Tools & references
GoF catalog, "Patterns of Enterprise Application Architecture" (Fowler), refactoring.guru.
