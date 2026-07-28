# Docker

## Scope
Building, optimizing, and running containerized applications — image construction, layering, registry interaction, and runtime configuration.

## Core principles
- Containers are immutable artifacts with fixed dependencies; the trade-off is that layers are permanent — bloat in layer N means every derivative inherits it.
- Use multi-stage builds to separate compile environments (large, with toolchains) from runtime environments (minimal, only binaries and runtime) — image size should be measured in tens, not hundreds, of MB.
- Alpine and distroless images reduce attack surface and startup time; avoid "slim" — that's still 100+ MB of apt metadata.
- Keep the Dockerfile stable while pushing logic into shell scripts or build-time composition — the Dockerfile is read more than it's executed.
- Image registries are the artifact source-of-truth; tagging discipline (semantic versioning, git SHA) is as critical as code versioning.

## Apex practices
- Build images locally, store layer metadata, and fail the build if size regressions exceed a threshold — catching bloat early prevents deployment surprises.
- Use build cache with `--cache-from` and layer-specific bind-mounts to avoid rebuilding unchanged layers; structured Dockerfiles (dependencies before source) maximize cache hits.
- Sign and scan container images in the registry (Cosign, Trivy, Anchore) before they're deployed; vulnerability in the supply chain beats vulnerability in code.
- Run containers with the minimal privilege set: non-root user, read-only root filesystem where possible, dropped capabilities (CAP_DROP ALL then CAP_ADD only what's needed).

## Pitfalls
- Storing secrets in image layers (environment, hardcoded files) — they persist in layer history even if deleted later; use build-time secrets and runtime injection.
- Treating `docker run` as production — compose services together early with `docker-compose` or move to orchestration; spot testing never finds integration issues.
- Optimizing for build time when runtime is the pain point — a 5-minute build that saves 100ms per container startup on a fleet of 10k instances is not a win.

## Tools & references
Dockerfile best practices (official), docker buildx for multiarch, Trivy for scanning, Sigstore for signing, OCI image spec.
