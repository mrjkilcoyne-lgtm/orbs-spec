# Developer Experience

## Scope
Making the developer workflow smooth: local development, inner loop iteration, and operational friction reduction.

## Core principles
- Developer velocity is a quality metric — if development iteration is slow (slow feedback loops, complex setup, brittle tests), bugs accumulate and ship time increases.
- Local development should mirror production (same services, same versions, same configurations) or divergence hides bugs — Docker Compose or Tilt solve this.
- Setup friction (first-day experience, onboarding latency) compounds across all developers — invest in good documentation and automation (makefile, setup scripts).
- Debugging is a first-class concern — developers need visibility into what their code does (logs, traces, metrics) and how to reproduce production issues locally.
- Feedback must be fast (seconds for unit tests, minutes for integration tests) or developers context-switch and bugs multiply.

## Apex practices
- Invest in local development tooling (Tilt, Skaffold, Nix) that mirrors production and rebuilds fast — save developers minutes per iteration loop × hundreds per year.
- Provide runbooks for common operations (how to run the migration, how to test a feature flag locally, how to debug a timeout) — documentation is cheaper than repeated Slack questions.
- Make common developer workflows scriptable (test a single service, deploy a branch to a dev environment, run a service locally pointing to staging dependencies) — codify in shell scripts or Makefiles.
- Instrument development environments with the same observability as production (same logging, metrics, tracing) — a dev can then test "does my code log the right thing?" before shipping.

## Pitfalls
- Assuming production debugging is sufficient (devs add print statements in prod code) — local reproducibility saves time and risk.
- Making local environment setup require 30+ steps (documentation rot, inconsistent setups) — automate it; use Dockerfile or bootstrap scripts.
- Slow feedback (deploy to staging to test a feature) — iterate locally, deploy to staging only when confident.

## Tools & references
Tilt, Skaffold, Docker Compose, Nix, Earthly, LocalStack for AWS simulation, Devbox for environment management.
