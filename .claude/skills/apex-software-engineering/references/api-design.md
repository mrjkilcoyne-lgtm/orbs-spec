# API Design

## Scope
Designing programmatic interfaces (libraries, services, modules) that are easy to use correctly and hard to misuse.

## Core principles
- Design from the caller's perspective: write the calling code first.
- Make illegal states unrepresentable — encode invariants in types/signatures.
- Minimize surface area; every public symbol is a forever commitment.
- Be conservative in what you emit, explicit in what you accept; validate at the boundary.
- Consistency beats local optimality: same concepts, same names, same shapes everywhere.

## Apex practices
- Version deliberately; additive changes only within a major version.
- Provide escape hatches (raw access, options structs) so the 90% case stays simple.
- Document behavior contracts (idempotency, ordering, error semantics), not just parameters.
- Dogfood: build a real consumer before freezing the interface.

## Pitfalls
- Boolean parameters that read as `doThing(true, false)` at call sites.
- Leaking internal types/exceptions through the public boundary.
- Breaking changes hidden as "bug fixes."

## Tools & references
"A Philosophy of Software Design" (Ousterhout), API evolution guides (Go, Java), OpenAPI for HTTP surfaces.
