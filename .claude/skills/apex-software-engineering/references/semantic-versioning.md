# Versioning & Compatibility

## Scope
Communicating change through version numbers and managing compatibility promises.

## Core principles
- SemVer is a contract: MAJOR breaks, MINOR adds, PATCH fixes — from the consumer's perspective, not yours.
- Anything observable can be depended on (Hyrum's Law); "internal" behavior changes can still break users.
- Breaking changes are a cost you impose on every consumer; batch them and provide migration paths.
- Pre-1.0 signals instability, but users will depend on it anyway — act accordingly.
- Deprecate before removing: warn in N, remove in N+1, with the replacement named in the warning.

## Apex practices
- Maintain a CHANGELOG written for humans: grouped by added/changed/fixed/removed, with migration notes.
- Gate releases with API-diff tooling that flags accidental breaking changes.
- Support the previous major long enough for realistic migration (state the window).
- Version schemas, protocols, and file formats — not just code.

## Pitfalls
- "Just a small breaking change" in a minor release.
- Version bumps without changelog entries, forcing users to read diffs.
- Coupling deploy version to API version in services — they evolve on different clocks.

## Tools & references
semver.org, Keep a Changelog, apidiff/revapi tooling, release-please/changesets automation.
