# Documentation

## Scope
Writing and maintaining docs that transfer understanding: READMEs, API refs, ADRs, runbooks, comments.

## Core principles
- Docs have four distinct jobs (Diátaxis): tutorials, how-to guides, reference, explanation — don't mix them in one page.
- Write for the reader's moment of need, not the author's moment of pride.
- The closer docs live to code, the more likely they stay true; prefer doc comments and in-repo markdown.
- Comments explain why (constraints, trade-offs, gotchas); the code itself says what.
- Wrong docs are worse than no docs — every doc needs an owner and a staleness check.

## Apex practices
- Write the README before the code settles: what it is, quickstart in 5 commands, where to go next.
- Record decisions as ADRs: context, options, decision, consequences — future maintainers inherit the why.
- Test your docs: a new person following the quickstart is the only real validation.
- Delete or archive stale docs aggressively; a small true corpus beats a large doubtful one.

## Pitfalls
- Documenting the obvious while the tricky invariant goes unwritten.
- Screenshots and version-pinned examples that rot silently.
- One giant wiki page that is tutorial, reference, and changelog at once.

## Tools & references
Diátaxis framework, ADR templates, docs-as-code toolchains (MkDocs, Docusaurus), vale for prose linting.
