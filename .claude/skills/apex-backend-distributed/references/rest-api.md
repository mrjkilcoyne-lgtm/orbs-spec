# REST API Design

## Scope
HTTP APIs modeled on resources: URIs, methods, status codes, evolution.

## Core principles
- Resources are nouns, methods are verbs: GET reads, POST creates/acts, PUT replaces, PATCH modifies, DELETE removes — and their safety/idempotency properties are contracts.
- Status codes are the protocol's error taxonomy: 2xx success, 4xx caller's fault (be specific: 400/401/403/404/409/422/429), 5xx yours — clients branch on them.
- Statelessness scales: every request self-contained (auth token, no server session affinity).
- Consistency across the surface: same pagination, filtering, error shape (RFC 9457 problem+json), naming everywhere.
- Design for evolution: additive changes, tolerant readers, explicit versioning strategy chosen before v1 ships.

## Apex practices
- Paginate every collection from day one (cursor-based for stability under writes); never return unbounded lists.
- Use ETags/If-Match for optimistic concurrency on updates; Location headers on 201.
- Document with OpenAPI as source of truth; generate clients/server stubs and validate requests against it.
- Model long-running operations explicitly (202 + status resource), not 30-second blocking requests.

## Pitfalls
- Tunneling everything through POST /doAction RPC-style, then calling it REST.
- 200 OK with {"error": ...} bodies breaking every generic client.
- Chatty resource granularity forcing N+1 client calls (design for use cases, allow expansion).

## Tools & references
OpenAPI, RFC 9110 (HTTP semantics), RFC 9457 (problem details), Stripe/GitHub API design as canon.
