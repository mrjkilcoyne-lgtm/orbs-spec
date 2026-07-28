# Service Catalogs

## Scope
Maintaining an inventory of available services, infrastructure, and capabilities: discovery, documentation, and self-service provisioning.

## Core principles
- A service catalog is the single source of truth for what infrastructure and services are available — if it's not in the catalog, it doesn't exist as far as the organization knows.
- Discovery is not optional — developers need to know what's available before they build it themselves; lack of discovery leads to duplication and reinvention.
- Ownership is explicit — every service has an owner (team) responsible for upgrades, support, and retirement.
- The catalog evolves with the organization — as new services are adopted or deprecated, the catalog reflects current state; stale catalogs are useless.
- Self-service automation connects discovery to provisioning — a developer finds a service in the catalog and provisions access or an instance with one click.

## Apex practices
- Use a tool (Backstage, Humanitec, LaunchPad) that integrates with your infrastructure provisioning (Terraform, Kubernetes, Helm) so that provisioning via the catalog is reliable.
- Include metadata per service (owner, SLO, runbook, architecture diagram, cost, dependencies) so developers understand trade-offs.
- Track and retire unmaintained services (no owner, no SLO, stale documentation) — they become technical debt and security liabilities.
- Version and audit changes to the catalog (who provisioned what, when was it modified?) — compliance and incident investigation require this.

## Pitfalls
- Catalog that's beautiful but incomplete (covers 30% of infrastructure, users still manage other services manually) — it becomes context-switching overhead.
- Provisioning via the catalog requires manual follow-up or tickets to ops (breaks self-service) — the catalog is only useful if provisioning is fully automated.
- No enforcement (teams can ignore the catalog and set up services manually) — adoption requires that the catalog is easier than the alternative.

## Tools & references
Backstage, Humanitec, LaunchPad, Port.io, CloudCraft, CNCF Cloud Native Landscape, service mesh service discovery.
