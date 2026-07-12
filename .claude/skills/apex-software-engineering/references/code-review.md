# Code Review

## Scope
Reviewing changes for correctness, clarity, and design fit — and authoring changes that review well.

## Core principles
- Review the behavior and its edge cases first; style last (and ideally automated away).
- Small PRs get better reviews; review quality falls off a cliff past ~400 lines.
- The author owns the code; the reviewer owns catching what the author can't see.
- Comments distinguish blocking issues from suggestions ("nit:", "non-blocking:").
- A review is a conversation, not a gate check; explain the why behind requests.

## Apex practices
- As author: write the PR description as a guided tour — what, why, how to verify, what you're unsure about.
- Verify claims, don't assume: check the failure path, the test actually asserts, the migration is reversible.
- Approve with comments when issues are minor; don't hold hostage over taste.
- Track recurring review feedback and turn it into lint rules or docs.

## Pitfalls
- Rubber-stamping large diffs because reviewing them properly feels impossible.
- Bikeshedding naming while an unhandled error path ships.
- Relitigating architecture in review that was decided in design.

## Tools & references
Google's Code Review Developer Guide, Conventional Comments, danger/reviewdog for automation.
