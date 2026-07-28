# Secrets Hygiene

## Scope
Managing credentials, API keys, and cryptographic material across their lifecycle: storage, distribution, rotation, and leak response.

## Core principles
- Secrets in git are permanent: history survives force-pushes in forks, clones, and caches, so a committed secret is a rotated secret — cleaning history is forensics, not remediation.
- The hierarchy of secret quality: no secret (IAM roles, workload identity, OIDC federation between platforms) > short-lived dynamic secrets (Vault database credentials, STS tokens) > long-lived secrets in a vault > env vars > files > code. Every design decision should move up this ladder.
- Rotation must be a routine, tested, zero-downtime operation — if rotating your DB password requires a maintenance window, you won't rotate during an incident, which is exactly when you must.
- Environment variables are a weak container: they leak into crash dumps, `/proc/<pid>/environ`, child processes, and debug endpoints; prefer file mounts with tight permissions or direct vault API fetch at startup.
- Detection is a race you must enter: secret scanning in pre-commit, in CI, and against the org's entire history (public leak monitoring included) — attackers scan public GitHub for AWS keys in under a minute.

## Apex practices
- Use CI/CD workload federation (GitHub Actions OIDC → cloud STS) instead of storing long-lived cloud keys as CI secrets — the single highest-leverage secrets improvement in most orgs.
- Give every secret an owner, an inventory entry, a rotation SLA, and audit logging on access; an unowned secret is an unrotatable one.
- Practice the leak drill: from "secret found in public repo" to "rotated and old value dead" should be minutes; keep a per-secret revocation runbook.
- Bake nothing into images or AMIs; inject at runtime via CSI secrets driver, Vault agent sidecar, or cloud secret manager, and scan images (trufflehog, gitleaks) to verify.

## Pitfalls
- "Rotated" the secret but old value still works — rotation without revocation, common with API keys that allow multiple active values.
- Secrets in Kubernetes ConfigMaps, Helm values files, or terraform state in a world-readable bucket — state files contain every secret terraform ever touched.
- Sharing one credential across services or humans, destroying attribution and making rotation a coordinated multi-team event.

## Tools & references
HashiCorp Vault, AWS Secrets Manager / SSM Parameter Store, GCP Secret Manager, SOPS + age, gitleaks, trufflehog, GitHub secret scanning + push protection, external-secrets-operator.
