# Terraform & Infrastructure as Code

## Scope
Declarative infrastructure provisioning: resource graphs, state management, module composition, and drift detection.

## Core principles
- Terraform state is the source of truth for what exists; losing state means losing track of infrastructure, which creates orphaned resources and manual cleanup.
- State must be protected (remote backend with encryption and versioning), never committed to Git, and never edited manually (replace, delete via code instead).
- Immutable infrastructure (replace resources rather than mutate them in place) is the only safe way to apply Terraform — mutating in place hides the real configuration.
- Modules abstract infrastructure patterns but can become a leaky abstraction; well-designed modules hide complexity and expose a narrow interface, poorly-designed ones expose all the knobs.
- Plan before apply; `terraform plan` is documentation, not just a preview — review it carefully, version it (in PR), and use it for approval gates.

## Apex practices
- Use workspaces or separate state files for dev/staging/prod, never share state across environments (a typo in prod still uses prod state).
- Implement approval gates on `terraform apply` to prod; require plan review in the PR, sign-off from a second person, and immutable audit logs of who approved what.
- Parameterize via variables.tf with clear defaults and validation; locals for computed/private values — the interface should be obvious.
- Test terraform with `terraform plan` against a real (dev) backend and check for unintended deletions before shipping; `terraform destroy` on a PR is a safety net.

## Pitfalls
- State drift from manual changes (console clicks outside Terraform) — detection and recovery are painful; lock infrastructure from manual edit immediately.
- Modules that expose every resource output (tight coupling to implementation) — internal details change, breaking downstream code.
- Running `terraform apply` without reviewing the plan; Terraform is declarative but not omniscient — computed values and datasources can surprise.

## Tools & references
Terraform Registry, Terratest for infrastructure testing, Atlantis for GitOps terraform, tfenv for version management, checkov for policy enforcement.
