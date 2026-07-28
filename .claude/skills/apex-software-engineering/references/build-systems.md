# Build Systems

## Scope
Turning source into artifacts: compilation, bundling, caching, and reproducibility.

## Core principles
- Builds must be deterministic: same inputs, same outputs — this unlocks caching and trust.
- The dependency graph is the build system; undeclared inputs cause the "works on my machine" class of bugs.
- Incremental correctness beats incremental speed: a fast wrong build costs more than a slow right one.
- Hermetic builds (pinned toolchains, no network at build time) make CI and laptops agree.
- Build time is a tax on every engineer, every day; treat it as a product with a budget.

## Apex practices
- Content-hash caching (local and remote) so unchanged targets never rebuild.
- Fail the build on warnings you care about; a warning ignored for a year is policy.
- Keep a single entry point (`make build`, one script) so CI and humans run the identical path.
- Measure and graph build times; fix the critical path, not the average.

## Pitfalls
- Glob-everything targets that rebuild the world on any change.
- Logic living only in CI YAML, unrunnable locally.
- "Clean build fixes it" accepted as normal — that's a missing dependency edge.

## Tools & references
Bazel/Buck2, Gradle, Nix, Make done well, Turborepo/Nx for JS monorepos.
