# Configuration Management

## Scope
Managing and propagating application and infrastructure configuration across environments: version control, hot-reload, validation, and drift.

## Core principles
- Configuration is code; it must be versioned, reviewed, and audited — configuration drift (what's deployed vs. what's in Git) is debt that compounds.
- Secrets and non-secrets have different lifecycle requirements; never version secrets, use runtime injection, and rotate them independently of non-secret config changes.
- Configuration changes must be testable before production — if you can't validate a config change in staging first, you're not ready to deploy to prod.
- The single source of truth for environment configuration is the deployment artifact or the system state file (Terraform state, k8s manifests), not spreadsheets or docs.
- Configuration layers (global → environment → service → feature flags) should be explicit and ordered; implicit fallbacks hide what config is actually active.

## Apex practices
- Use environment variables for runtime config (12-factor), not config files — but validate and type them at startup (not silently defaulting to wrong values).
- Implement configuration validation at deploy time (schema validation, permission checks, connectivity tests) so bad config fails fast and visibly.
- Support hot-reload for non-critical configuration (feature flags, rate limits, log levels) — require a deploy for configuration changes that affect correctness (database URLs, API keys).
- Centralize configuration for multi-service systems (Consul, etcd) only when you need cross-service coordination; GitOps (Flux, ArgoCD) is usually simpler.

## Pitfalls
- Configuration stored in multiple places (Git, Terraform, k8s ConfigMaps, environment variables) without a source-of-truth — production has X, staging has Y, nobody knows why.
- Hot-reload without validation — a typo in a rolled-back config crashes all instances.
- No rollback plan for configuration changes — if a config change breaks everything, can you revert in under 5 minutes?

## Tools & references
Kubernetes ConfigMaps, etcd, Consul, Vault for secrets, feature flag systems (LaunchDarkly, Unleash), 12-factor app methodology.
