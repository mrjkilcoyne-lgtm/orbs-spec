# Landing Zones & Enterprise Cloud Setup

## Scope
Establishing secure, scalable cloud foundations for organizations: account structure, governance, and compliance.

## Core principles
- A landing zone is foundational infrastructure (networking, IAM, logging, monitoring) provisioned before applications; it sets the guardrails for the whole organization.
- Account structure (one account per environment, team, workload) enables isolation and billing attribution; it's hard to undo, plan early.
- Governance (organizations policies, SCPs, centralized logging) enforces compliance from the start; retrofitting governance is painful.
- Network design (VPC layout, subnets, connectivity) is harder to change later; multi-account architecture requires explicit cross-account networking.
- Shared services (centralized logging, monitoring, DNS, NAT) reduce operational burden but create dependencies; architecture for resilience.

## Apex practices
- Use cloud provider landing zone frameworks (AWS Control Tower, GCP Cloud Landing Zone, Azure Landing Zones) as a starting point, then customize.
- Implement a hub-and-spoke network topology for multi-account deployments: a central account (hub) for shared services, spoke accounts for workloads, traffic routed through hub.
- Centralize logging (CloudTrail, VPC Flow Logs, application logs) in a separate account that nobody else can modify; compliance requires immutable audit trails.
- Automate everything (infrastructure as code) so the landing zone is reproducible and versioned; manual setup is slow and error-prone.

## Pitfalls
- Single account for everything (no isolation, hard to audit, blast radius is the entire organization) — use multi-account from day one.
- Complex network topology without documentation (nobody understands traffic flow, troubleshooting is hard) — document and diagram.
- No plan for scaling (landed with 5 accounts, now need 100; the account structure becomes a bottleneck) — design for growth.

## Tools & references
AWS Control Tower, AWS Landing Zone Accelerator, GCP Cloud Landing Zone, Azure Enterprise Scale, Terraform, infrastructure as code best practices.
