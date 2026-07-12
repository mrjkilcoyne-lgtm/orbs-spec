# Azure Core

## Scope
Fundamental Azure services and architectural patterns: VMs, Virtual Networks, IAM, and managed services.

## Core principles
- Azure subscriptions are the billing and administrative boundary; multi-subscription architecture is common for large organizations (one per environment, team, cost center).
- Azure regions have paired regions (for disaster recovery); data can't replicate across regions automatically so design multi-region explicitly.
- Availability sets and zones provide redundancy; managed disks handle underlying replication, but you must choose where instances run.
- Azure RBAC is granular but differs from other clouds in scope (role, scope = resource group/subscription, not path-based like AWS).
- Managed services (App Service, Azure Database, Cosmos DB) handle scaling and patching; VMs require more manual management.

## Apex practices
- Use managed services where possible (Azure App Service for web, Azure SQL for databases) to reduce operational burden.
- Implement Azure Policy to enforce governance (allowed SKUs, required tags, network configuration) at the subscription level.
- Use managed identities (system-assigned or user-assigned) instead of connection strings or keys for service-to-service auth.
- Organize subscriptions by environment or team; use management groups for consistent policy across multiple subscriptions.

## Pitfalls
- Single-zone deployments (zone fails, workload goes down) — always use availability zones or sets.
- Using connection strings embedded in code (security risk, hard to rotate) — use managed identities or key vaults.
- Ignoring Azure's regional differences (some services unavailable in certain regions) — check region availability early.

## Tools & references
Azure documentation, Terraform Azure provider, Azure CLI, Azure DevOps, "Exam AZ-900" study materials for conceptual overview.
