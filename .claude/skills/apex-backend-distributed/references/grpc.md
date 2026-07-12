# gRPC & Protobuf

## Scope
Contract-first binary RPC: protobuf schemas, streaming, deadlines, service evolution.

## Core principles
- The .proto file is the contract and the documentation: field numbers are forever, names are cosmetic.
- Schema evolution rules are mechanical: never reuse/renumber fields, reserve removed ones, additive changes only — breaking these corrupts data silently.
- Deadlines propagate: every call carries one, servers respect and forward them; a missing deadline is an infinite hang waiting.
- Four call shapes (unary, server-stream, client-stream, bidi) — streams for large/live data, unary for everything else.
- Status codes are richer than HTTP: use canonical codes (NOT_FOUND, FAILED_PRECONDITION, RESOURCE_EXHAUSTED) precisely; clients retry on them.

## Apex practices
- Buf for linting/breaking-change detection in CI — schema discipline automated.
- Design idempotent methods where retries happen; mark them, and configure retry policy in service config not ad-hoc client loops.
- Use interceptors for cross-cutting concerns (auth, telemetry, validation) — the middleware layer.
- Load-balance client-side or via proxy that understands HTTP/2 (L7): naive L4 balancing pins all traffic to one backend per connection.

## Pitfalls
- Reusing a deleted field number (old data decodes as the new field).
- Streaming when unary + pagination was simpler, then debugging flow control.
- Trusting default zero-values to mean "unset" where absence matters (use optional/wrappers).

## Tools & references
protobuf docs (proto3), buf.build, grpc.io guides, grpcurl for debugging.
