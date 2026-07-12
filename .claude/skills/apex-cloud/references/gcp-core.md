# GCP Core

## Scope
Fundamental GCP services and architectural patterns: Compute Engine, VPC, IAM, and App Engine/Cloud Run workload options.

## Core principles
- GCP projects are the billing and permissions boundary — multi-project architecture is common for multi-tenancy or environment separation.
- Compute options span a spectrum: VMs (control) → App Engine standard (managed) → Cloud Functions (serverless); choose by your requirements, not by fashion.
- VPC is shared across projects via shared VPC; complex networking requires planning early (subnets, firewall rules, routes).
- Workload Identity (OIDC-based service accounts) is the secure way to grant access — long-lived service account keys are a security risk.
- GCP's default quotas per region are conservative; plan for multi-region early and raise quotas before you hit them.

## Apex practices
- Use Cloud Run for stateless services (autoscales from zero, cost only when running) and Firestore/Datastore for automatic scaling needs.
- Implement organization policies at the org level to enforce compliance (e.g., block public IPs, require encryption, restrict regions).
- Use Workload Identity Binding to grant Kubernetes pods GCP permissions — no keys on containers, credentials are short-lived.
- Leverage GCP's integrated billing, logging, and monitoring; use the same identities and permissions across all services.

## Pitfalls
- Using default VPCs or permissive firewall rules (anything → anything) — lock down from the start.
- Workloads in a single region (if the region has issues, you're offline) — design for multi-region failover.
- Ignoring quota limits (hitting soft limits mid-deployment) — request quota increases before they're needed.

## Tools & references
GCP documentation, Terraform GCP provider, Cloud Console, gcloud CLI, "Google Cloud Platform in Action" by Geewax.
