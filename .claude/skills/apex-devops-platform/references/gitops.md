# GitOps

## Scope
Using Git as the single source of truth for infrastructure and application state, with automatic convergence between declared and actual state.

## Core principles
- Git is the audit log and approval mechanism — every change is a commit with history, review, and blame; drift from Git state is treated as a failure, not a feature.
- Declarative over imperative — push desired state to Git, let controllers converge the cluster, not manual deployments or scripts.
- Separation of concerns: Git holds desired state (what you want), controllers handle convergence (how to get there), monitoring detects drift (is there a gap).
- Pull-based (in-cluster operator) beats push-based (external orchestrator); the cluster asks Git for updates, never trusting an external system to trigger changes.
- GitOps requires idempotent operations — the same manifest applied twice must be safe, or drift recovery will fail or cause cascading failures.

## Apex practices
- Use a GitOps operator (ArgoCD, Flux) that watches Git and syncs continuously; configure sync policies to detect drift, alert on divergence, and auto-remedy or require manual approval.
- Structure Git repos by environment/cluster or by team/application depending on your deployment topology; document the structure so operators know where to change what.
- Implement promotion pipelines in Git: commit to dev branch, CI runs, on merge to staging branch it deploys to staging, on merge to main it deploys to prod (branch protection ensures review).
- Version your infrastructure manifests and track rollbacks in Git — a rollback is a commit, not a flag; your Git history shows the exact state at any point in time.

## Pitfalls
- Mixing push and pull (some changes via GitOps, some via kubectl apply) — Git becomes stale and operators don't trust it.
- GitOps applied only to manifests, not to infrastructure provisioning (Terraform) — you're managing half the system, the other half is manual.
- No drift alerting or auto-remediation — Git and cluster diverge silently, discovered only in an incident.

## Tools & references
ArgoCD, Flux CD, GitHub Actions for promotion, sealed-secrets or external-secrets for secret injection, CNCF GitOps whitepaper.
