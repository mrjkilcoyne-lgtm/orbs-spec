# Release Management

## Scope
Planning, coordinating, and executing versioned releases: versioning strategy, changelog maintenance, and release notes.

## Core principles
- Releases are semantic milestones, not just deployments — a version tag says "this code is stable, tested, and customer-ready" (or internal-milestone-ready).
- Versioning discipline (major.minor.patch) communicates stability — callers can update a minor version with confidence, knowing breaking changes only come in majors.
- Releases must be traceable: a version tag points to a specific commit, which points to specific artifacts and deployment — reproducibility requires this chain.
- Release notes are not optional — they document what changed, why it changed, and what customers need to know (upgrade steps, breaking changes, security fixes).
- Release frequency is a quality signal — daily releases with small changes are safer and faster than monthly releases with 100 changes; velocity enables safety.

## Apex practices
- Use semantic versioning (major.minor.patch); automatically bump patch on patch branches, minor on feature branches, major for breaking changes.
- Maintain a changelog (CHANGELOG.md) updated with every merge; generate release notes from the changelog automatically.
- Tag releases in Git with annotations (tagger, date, message); the tag is immutable and auditable, unlike release notes edited later.
- Automate release creation (cut a tag in Git, CI builds and publishes artifacts, release notes are generated and published); manual releases are slow and error-prone.

## Pitfalls
- No versioning discipline (all commits are "latest") — users can't distinguish between stable and development versions.
- Release notes written after the fact from git log (they're generic and unhelpful) — write during development or extract from structured commit messages.
- Releasing without being able to roll back (if the release breaks things, you're stuck) — always test releases in staging first.

## Tools & references
Git tags, conventional commits, semantic-release, Changesets, Release Please, GitHub Releases, SemVer.org, "Accelerate" release practices.
