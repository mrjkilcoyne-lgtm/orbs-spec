# Artifact Registries

## Scope
Storing, versioning, and distributing build artifacts (containers, binaries, packages): registry architecture, access control, and supply chain security.

## Core principles
- Artifacts are immutable once tagged — a tag points to a specific build forever, which is the only way to guarantee reproducibility (no "latest" chaos in production).
- Registry access is a security boundary — who can pull (runtime), who can push (CI/CD), who can delete (operators), and who can see metadata (security scanners) should be granular.
- Digests (SHA256 of the artifact) are tamper-proof pointers; tags (semver, "latest") are human-readable but can be rettagged; signing artifacts proves they came from a trusted builder.
- Retention policies prevent unbounded storage (hundreds of builds per day × years = petabytes) — but deleting a tag that's in-use in production is a disaster.
- Registry availability is availability of your deployments — a flaky registry breaks deployments, forcing operators to use stale cache; it must be as reliable as your database.

## Apex practices
- Tag artifacts with git commit SHA and semantic version; push all tags, then promote in GitOps (tag "staging" → "production" in the registry, not rebuilding).
- Sign artifacts at build time (Cosign + OIDC) and enforce signature verification at deploy time; prevents supply chain injection if a builder is compromised.
- Scan artifacts for vulnerabilities before deployment (Trivy, Grype) — catch them before they reach production, gate deployment on policy (fail on critical CVEs).
- Implement pull-through caches (local registry proxying upstream registries) to reduce dependency on external registries and speed up deployments.

## Pitfalls
- Using "latest" tag in production (forces redeployment of stale images, breaks immutability, defeats the purpose of versioning).
- No retention policy (unbounded storage costs and regulatory issues if deleted data is mandated to exist).
- Scanning only at deploy time (too late); scan during build, fail the build, never tag a vulnerable image.

## Tools & references
Harbor (enterprise registry with RBAC and scanning), Docker Registry, Artifactory, Quay, OCI Distribution Spec, Sigstore for signing and verification.
