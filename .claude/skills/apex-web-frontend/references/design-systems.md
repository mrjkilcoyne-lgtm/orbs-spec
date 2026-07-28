# Design Systems

## Scope
Shared component libraries, tokens, and the practices that keep product UI coherent at scale.

## Core principles
- A design system is a product with users (product teams), not a component dump; adoption is its success metric.
- Tokens are the foundation: named decisions (color.action.primary) not values (#0055FF); semantic layer over raw palette.
- Components encode UX decisions (accessibility, states, spacing) so product teams can't easily rebuild them wrong.
- The API is the contract: composable primitives (slots/children) outlive prop-explosion monoliths.
- Versioned like a library: semver, changelogs, migration guides, deprecation windows — surprise breaking changes destroy trust.

## Apex practices
- Build on headless/accessible primitives (Radix, React Aria) — behavior correctness is the hardest 80%.
- Document with live examples (Storybook) including do/don't guidance; the docs are the system.
- Design escape hatches deliberately: className passthrough with guardrails beats forks in every product repo.
- Track adoption (telemetry on component usage) and treat detachment/forking as user feedback.

## Pitfalls
- Shipping the kitchen sink before nailing buttons, forms, and dialogs.
- Tokens that mirror the palette (blue500) instead of intent (surface.raised) — themes become impossible.
- Governance without contribution paths: teams blocked on the system team fork silently.

## Tools & references
Storybook, style-dictionary (tokens), Radix/React Aria, designsystems.com case studies.
