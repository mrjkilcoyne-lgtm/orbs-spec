# Code Generation

## Scope
Producing code from schemas, templates, or models: protobuf stubs, ORMs, scaffolds, macros.

## Core principles
- The schema/source-of-truth is the code you maintain; generated output is an artifact.
- Never hand-edit generated files; regeneration must be safe at any time.
- Decide once: commit generated code (reviewable, no toolchain needed) or generate in-build (always fresh) — and enforce it.
- Generated code must be deterministic and stable-ordered, or diffs become noise.
- Keep the generation boundary visible: headers ("DO NOT EDIT"), separate directories, lint exclusions.

## Apex practices
- Verify in CI that regenerating produces zero diff — catches drift and hand edits.
- Design extension points (partial classes, hooks, sibling files) so custom logic lives outside generated files.
- Version the generator with the schema; regenerating with a new generator is a change to review.
- Generate the boring 80% and keep the interesting 20% handwritten, not vice versa.

## Pitfalls
- Template logic so complex the generator is harder to maintain than handwritten code would be.
- Generated code that fails the project's own lint/type gates.
- Schema changes merged without regenerating downstream consumers.

## Tools & references
protoc plugins, OpenAPI generators, sqlc, quicktype, go:generate conventions.
