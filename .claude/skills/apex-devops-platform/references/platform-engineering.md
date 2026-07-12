# Platform Engineering

## Scope
Building internal developer platforms (IDP): abstractions, self-service APIs, and operational burden reduction for application teams.

## Core principles
- The goal is to reduce toil for application teams — standardized templates, automated provisioning, and self-service beat gatekeeping every request through ops.
- Platform teams own the API contract, not the implementation — teams consume "deploy my app" (abstraction), platform owns "how to provision and manage infrastructure" (implementation).
- Platforms must make the right thing easy and the wrong thing hard — sensible defaults, golden paths, and gentle guardrails (not hard blocks).
- Observability is non-negotiable — teams can't debug their platform; platform teams must expose metrics, logs, and traces for both the platform and applications it runs.
- Platform adoption is voluntary initially (migration incentives), then mandatory (ops stops supporting the old way) — this requires trust.

## Apex practices
- Start with a service catalog (infrastructure and services available as self-service) — Backstage, Launchpad, or custom — so teams know what exists.
- Provide scaffolding for common workloads (REST service, job, scheduled task, data pipeline) via templates — teams customize (timeouts, scaling, persistence), not build from scratch.
- Implement self-service infrastructure provisioning (teams request a Postgres database via the catalog, it's provisioned and access is granted automatically).
- Measure adoption and developer satisfaction; if adoption is low, investigate why — usually the platform is too opinionated or too slow to iterate.

## Pitfalls
- Building a platform nobody uses (overly opinionated, too slow, doesn't solve real problems) — talk to teams first about what toil they feel.
- Centralizing every decision (teams can't deploy a container without approval) — platforms should enable, not bottleneck.
- Platform becomes hard to maintain (bespoke, undocumented, single engineer knows it) — use off-the-shelf solutions where possible.

## Tools & references
Backstage, LaunchPad, Humanitec, Shareplex, CNCF Platform Engineering whitepaper, Team Topologies for organizational design.
