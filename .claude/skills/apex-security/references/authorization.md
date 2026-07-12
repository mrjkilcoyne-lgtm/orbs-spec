# Authorization

## Scope
Deciding what an authenticated principal may do: models (RBAC, ABAC, ReBAC), policy enforcement, and multi-tenant isolation.

## Core principles
- Authorization must be enforced server-side at the resource, on every request — hiding buttons client-side or checking only at the route level invites IDOR and forced browsing.
- Pick the model that matches the question: RBAC answers "what does this role do," ABAC answers "under what conditions," ReBAC (Zanzibar-style relationship tuples) answers "who can act on this specific object" — document sharing is ReBAC, not a role explosion.
- Default deny with least privilege: absence of a grant is a denial; policies enumerate what is allowed, never what is forbidden.
- Centralize the policy decision point and distribute enforcement: one policy engine (OPA, Cedar, SpiceDB) queried by many services beats forty ad-hoc if-statements that drift apart.
- The confused deputy is the classic distributed failure: service A must not perform actions for user U beyond U's rights just because A itself is privileged — propagate the end-user context (token exchange, on-behalf-of) through the call chain.

## Apex practices
- Route every object access through a single authorize(subject, action, resource) chokepoint; a grep for direct DB access that bypasses it is a standing code-review check.
- Write authorization tests as a matrix — every (role, endpoint, ownership) combination including the negative cases; IDOR tests use two real tenants' data.
- Log every deny with subject, action, resource, and policy that fired; deny-spikes are an attack signal and the log is your audit trail.
- Model tenancy as a first-class attribute enforced at the data layer (row-level security, per-tenant key prefixes), not just in application filters.

## Pitfalls
- Role explosion: encoding resource instances into roles ("editor-of-project-1234") until RBAC collapses — that is the signal to move to ReBAC.
- Checking authorization on read but not on the mutation path (or vice versa), or forgetting non-CRUD surfaces: exports, webhooks, background jobs, GraphQL resolvers.
- Caching an allow decision past a revocation event — permission changes must bound cache TTLs or trigger invalidation.

## Tools & references
Google's Zanzibar paper, OPA/Rego, AWS Cedar, SpiceDB/Ory Keto, OWASP Authorization Cheat Sheet, XACML for the ABAC vocabulary.
