# Cost Optimization

## Scope
Reducing cloud and infrastructure spending without sacrificing reliability: rightsizing, reserved instances, spot instances, and waste identification.

## Core principles
- Cost has a signal function — high costs indicate inefficiency (idle resources, wrong instance types, compute in wrong region) that should be investigated, not just paid.
- Spot instances and preemptible VMs are commodity economics — use them for batch/non-critical workloads, but never for workloads without graceful shutdown or retry logic.
- Reserved instances lock you into a price; use them for baseload (production database, always-on services), not for variable workloads (test environments, canaries).
- Most cloud bills are dominated by 10% of resources — find and optimize the top spenders (often data transfer, storage replication, or misconfigured auto-scaling).
- Chargeback (billing teams/services for their resource consumption) creates incentives to optimize; shared cloud accounts with no attribution lead to waste.

## Apex practices
- Rightsize instances using historical CPU/memory utilization — a t3.xlarge running at 10% utilization should be a t3.medium; use tools (Compute Optimizer, etc.) or manual review.
- Use savings plans (1-3 year commitment) for predictable production workloads; switch to spot/preemptible for development and batch jobs.
- Implement resource tagging by cost center and workload type, then track spend by tag; tag everything at creation time (enforce via IaC).
- Automate cleanup (delete abandoned resources, stop idle databases, expire old snapshots) — manual cleanup doesn't scale and forgetfulness costs money.

## Pitfalls
- Optimizing cost at the expense of reliability (no redundancy, single instance) — a 50% cost reduction that causes an outage is not a win.
- No cost visibility (nobody knows what workloads cost) — you can't optimize what you don't measure.
- Reserved instances for highly variable workloads (paying for capacity you don't use) — use on-demand or spot with autoscaling instead.

## Tools & references
AWS Cost Explorer, GCP Billing, Azure Cost Management, Infracost for Terraform, CloudSecure, FinOps Foundation, cdk8s for cost-aware deployment.
