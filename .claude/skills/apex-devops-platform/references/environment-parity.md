# Environment Parity

## Scope
Maintaining consistency between development, staging, and production environments to catch bugs before production.

## Core principles
- If development works but production fails, the environment difference is the bug — dev/staging/prod should be identical except for scale, replicas, and credentials.
- Infrastructure as Code (Terraform, k8s manifests) is the mechanism for parity — the same code provisions all environments, parametrized by environment name.
- Data parity is as important as infrastructure parity — a schema that's different in staging breaks migrations; refresh production data to staging regularly (anonymized).
- Immutable infrastructure makes parity easier — rebuild all machines from the same image rather than applying patches manually.
- Drift detection (comparing actual state to desired state) is the enforcement mechanism — run it nightly and alert on divergence.

## Apex practices
- Define environment configurations in Git (Terraform modules per environment or kustomize overlays); generate all environments from the same source.
- Refresh staging database from production nightly (anonymized, with sensitive data redacted) — tests against real schema and data shapes, not stale mocks.
- Use the same artifact (built once) across all environments — promote by tag or digest, not by rebuilding per environment.
- Run the same tests in staging that you run in production (smoke tests, performance tests, security scans) — if it passes staging it should pass prod.

## Pitfalls
- Environment-specific code (if env == "prod" { ... }) — this scales to unmaintainable quickly; parametrize instead.
- Staging treated as a free environment to experiment in — if staging breaks, you have no pre-production validation for production.
- Manual configuration drift (ops makes a change to production that isn't in code) — declare everything in Git or use drift detection to catch and remediate.

## Tools & references
Terraform, kustomize, Kubernetes namespaces, GitOps operators (ArgoCD, Flux), Environment variable promotion patterns, 12-factor app.
