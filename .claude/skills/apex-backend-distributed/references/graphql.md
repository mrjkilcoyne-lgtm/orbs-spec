# GraphQL

## Scope
Schema-first API layer: type system, resolvers, N+1s, federation.

## Core principles
- The schema is the product: types and fields model the domain graph for clients, not your database tables.
- Clients declare data needs; the server's job shifts to efficient fulfillment — resolver cost is invisible in the query shape.
- N+1 is the default failure mode: every list field with a nested resolver; DataLoader batching is not optional.
- Nullability is API design: non-null promises propagate errors upward; err toward nullable except where guaranteed.
- One graph, evolved not versioned: deprecate fields (@deprecated), add new ones, never break — the introspectable contract makes this tractable.

## Apex practices
- Design mutations as verbs with input/payload types and explicit user-error fields (not just top-level errors).
- Protect the server: depth limits, complexity budgets, persisted queries in production, timeouts per resolver.
- Cursor-based connections (Relay spec) for lists — retrofit is painful.
- Federation/schema-stitching only at real org scale; a modular monolith graph is simpler and usually enough.

## Pitfalls
- Exposing the ORM schema 1:1 (your DB migrations become breaking API changes).
- Unbounded queries from anonymous clients (the self-service DoS).
- Overfetching resolvers that load full entities to serve one field.

## Tools & references
graphql.org spec, DataLoader, Apollo/Yoga docs, Relay connection spec, escape-hatch REST for files/webhooks.
