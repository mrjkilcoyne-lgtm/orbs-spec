# Clean Architecture & Boundaries

## Scope
Structuring systems so dependencies point at the domain and details stay swappable.

## Core principles
- The dependency rule: source dependencies point inward — domain logic imports nothing about web, DB, or UI.
- Boundaries are defined by interfaces the inner layer owns; outer layers implement them (dependency inversion).
- Architecture is the set of decisions that are expensive to change; keep the cheap ones out of it.
- Screaming architecture: the top-level structure should say what the system does, not which framework it uses.
- Every boundary has a cost (indirection, mapping, ceremony); draw them where change actually happens.

## Apex practices
- Keep the domain model persistence-ignorant; map at the boundary rather than annotating entities into the DB.
- Enforce direction with tooling (import linters, module visibility), not convention alone.
- Defer detail decisions: a system that runs with an in-memory store proves the boundary is real.
- Start modular-monolith; extract services along proven boundaries, not speculative ones.

## Pitfalls
- Layer lasagna: five pass-through layers adding mapping but no decision.
- "Clean" folder names while imports crisscross every boundary.
- Abstracting the database you will never actually swap while coupling to the vendor SDK you will.

## Tools & references
"Clean Architecture" (Martin), hexagonal/ports-and-adapters (Cockburn), import-boundary linters (ArchUnit, dependency-cruiser).
