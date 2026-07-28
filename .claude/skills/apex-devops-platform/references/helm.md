# Helm

## Scope
Packaging and templating Kubernetes applications as reusable charts with versioning, dependency management, and release lifecycle.

## Core principles
- Helm charts are templates over manifests, not manifests over configuration; separating schema (chart) from values (environment data) is the whole point.
- Chart version and app version are independent — chart version bumps for structure changes, app version for the workload itself; mixing them hides what changed.
- Helm hooks (pre-install, pre-upgrade, post-delete) enable stateful operations (migrations, backups, cleanup) but are fire-and-forget; rely on them for safety only with explicit idempotency.
- Chart dependencies create a directed graph; conflicts (two charts need the same thing differently) are discovered late — lock dependency versions explicitly.
- Values override order matters (defaults → values.yaml → -f files → --set flags); document precedence or you'll ship unexpected configurations.

## Apex practices
- Structure charts with sensible defaults that work for dev; use values files for staging and prod that override selectively rather than redefining everything.
- Test helm output with `helm template` and validate against schema; a typo in values won't be caught until deploy time if you don't lint.
- Use helm test hooks to smoke-test deployments post-upgrade — verify connectivity, auth, basic functionality — before marking a release successful.
- Manage chart versions in a Git repo (chart storage) with semantic versioning; tag releases in Git so chart versions are auditable.

## Pitfalls
- Using Helm as a magic variable-substitution tool instead of designing charts for reuse — every environment gets its own values file that's a copy of the previous one.
- Setting no default values, requiring users to specify everything — unfriendly and error-prone.
- Helm hooks that aren't idempotent — re-running a release fails on the second attempt because the pre-install hook assumes a clean state.

## Tools & references
Helm docs (official), Helm Best Practices, Chart Testing, ChartMuseum for private registries, Helmfile for multi-chart orchestration.
