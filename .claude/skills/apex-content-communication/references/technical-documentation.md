# Technical Documentation

## Scope
Writing for engineers and technical audiences: clarity for implementation, completeness without encyclopedic bloat, and structure for scanning.

## Core principles
- Readers are trying to solve a problem, not learn your system; lead with the use case and show the happy path first, edge cases after.
- Audience skill level matters: docs for users are different from docs for contributors. Write one doc per skill level, not one doc for everyone.
- Examples beat explanation: a code snippet that works is worth 1000 words of prose. Executable, copy-paste examples are gold.
- Structure for scanning: headings, tables of contents, and quick-links let readers jump to what they need without reading sequentially.
- Keep it current; outdated docs (version numbers, API changes, deprecated methods) are worse than no docs because they mislead.

## Apex practices
- Use the "concept-task-reference" structure: explain what the thing is, show how to do common tasks with it, provide reference (parameters, options).
- Start with a "getting started" guide that works in 5 minutes; nothing kills adoption like a 2-hour setup.
- Include both minimal examples (bare-bones to understand the pattern) and production examples (real-world considerations).
- Write docs as if you're seeing the product for the first time; fresh eyes catch confusing jargon and missing steps.

## Pitfalls
- Assuming readers have context; spell out terminology or link to glossary. What's obvious to you is opaque to a newcomer.
- Writing in the future tense about features not yet built; keep docs in sync with code (automation via doc generation helps).
- Burying common questions in 50-page manuals; FAQ or prominent links solve 80% of support requests.

## Tools & references
Diátaxis documentation framework (tutorials, how-to guides, references, explanations), Read the Docs, Swagger/OpenAPI for API docs, MkDocs.
