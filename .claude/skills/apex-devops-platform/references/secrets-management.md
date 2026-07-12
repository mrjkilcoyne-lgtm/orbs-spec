# Secrets Management

## Scope
Protecting and distributing sensitive credentials (API keys, passwords, certificates): storage, rotation, access, and audit.

## Core principles
- Never version secrets in Git, even encrypted — encryption keys live somewhere; if you version encrypted secrets, you've just moved the problem.
- Secrets have a lifecycle: creation (with proper entropy), storage (encrypted at rest), delivery (encrypted in transit), use (never logged), rotation (regularly), and retirement (safe destruction).
- Access to secrets should be logged and auditable — a developer pulling an API key should generate an audit entry that security can review for anomalies.
- Secrets should be short-lived (use temporary credentials, issue time-limited tokens) when possible; long-lived static secrets are easier to compromise and harder to remediate.
- Delivery mechanism must be secure: in Kubernetes, use projected volumes or external-secrets (not environment variables logged by default).

## Apex practices
- Use a centralized secret manager (Vault, AWS Secrets Manager, GCP Secret Manager) with RBAC and audit logging — store the integration credentials in the platform, not in each app.
- Implement automatic rotation for long-lived secrets (every 30-90 days) with zero-downtime switchover (dual-write on rotation, single-read with failover).
- Use workload identity (Kubernetes IRSA, GKE Workload Identity) to issue temporary credentials to pods, not static keys mounted as files.
- Enforce encryption in transit (TLS 1.2+), at rest (AES-256), and in logs — strip secrets from logs automatically, fail builds if secrets are detected in code.

## Pitfalls
- Secrets in environment variables (visible in ps output, process inspection, logs) — use mounted files or secret APIs.
- No rotation (static secrets live forever, increasing compromise window) — a leaked key from 2019 still works in production.
- Manual secret distribution (ops copies a key to each machine) — error-prone and unauditable.

## Tools & references
HashiCorp Vault, AWS Secrets Manager, external-secrets Kubernetes operator, Sealed Secrets, Pulumi Secrets, OWASP Secret Management, CIS Benchmarks.
