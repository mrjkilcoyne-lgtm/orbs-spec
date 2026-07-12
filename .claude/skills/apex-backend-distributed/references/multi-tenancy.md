# Multi-Tenancy

## Scope
One system, many customers: isolation models, tenant context, noisy neighbors, data partitioning.

## Core principles
- The isolation spectrum — shared-everything (tenant_id column) → schema-per-tenant → database-per-tenant → stack-per-tenant — trades cost efficiency against isolation/compliance; choose per data-sensitivity tier, and know moves rightward are migrations, not flags.
- Tenant context is security-critical infrastructure: derive it from authenticated identity once at the edge, propagate it explicitly, and enforce it at the data layer (RLS, scoped repositories) — not by every developer remembering WHERE tenant_id.
- Cross-tenant data leakage is the existential bug class: defense in depth (query-layer enforcement + RLS + tests that attempt cross-tenant access) because one missed filter is a breach disclosure.
- Noisy neighbors are inevitable in shared tiers: per-tenant rate limits, quotas, and workload isolation (separate queues/pools for heavy tenants) — fairness is a feature you build.
- Tenant lifecycle is a product surface: provisioning, data export, deletion (with legal-grade completeness), and migration between tiers all need real implementations.

## Apex practices
- Postgres RLS (or equivalent) as the enforcement backstop with tenant set via session variable — the query that forgets the filter returns nothing instead of everything.
- Tag everything with tenant ID: logs, traces, metrics, costs — per-tenant observability answers "who is slow/expensive/broken" instantly.
- Test tenancy explicitly: automated cross-tenant access attempts in CI, per-tenant load tests for neighbor effects.
- Design for the whale early: your biggest tenant will need 100x the median — sharding keys and tier-migration paths chosen up front.

## Pitfalls
- Tenant ID from request parameters instead of the auth token (attacker-controlled tenancy).
- Shared caches/search indexes without tenant-scoped keys (leak via the side door).
- Hard-deleting a tenant without handling their rows in shared aggregate tables, queues, and backups.

## Tools & references
Postgres RLS docs, AWS SaaS Lens (well-architected), Citus for sharded tenancy, SaaS tenant-isolation whitepapers.
