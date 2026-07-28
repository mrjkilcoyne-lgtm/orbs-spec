# Dependency Management

## Scope
Choosing, updating, auditing, and removing third-party code.

## Core principles
- Every dependency is a liability with a maintenance schedule; adopt for core value, not convenience one-liners.
- Evaluate before adopting: maintenance activity, transitive tree size, license, security history, exit cost.
- Pin with lockfiles for reproducibility; update deliberately and frequently in small batches.
- The dangerous update is the one you defer for a year — small frequent upgrades keep each step cheap.
- Wrap risky dependencies behind your own interface so replacement is a local change.

## Apex practices
- Automate update PRs (Renovate/Dependabot) with CI as the gate; merge patch/minor routinely.
- Audit the transitive tree, not just direct deps; SBOM and vulnerability scanning in CI.
- Vendor or fork only with an explicit re-sync plan; a silent fork is a slow-motion incident.
- Periodically remove: unused deps, deps replaceable by stdlib, deps duplicating each other.

## Pitfalls
- left-pad risk: critical path on trivially replaceable micro-packages.
- Upgrading everything at once, then bisecting a week of breakage.
- Ignoring license obligations (GPL in proprietary code) until legal finds it.

## Tools & references
Renovate, Dependabot, osv-scanner/npm audit, license-checkers, deps.dev.
