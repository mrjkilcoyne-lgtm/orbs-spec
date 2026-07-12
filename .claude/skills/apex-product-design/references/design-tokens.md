# Design Tokens

## Scope
Systematic design scaling: token naming conventions, token systems, and implementation across platforms and tools.

## Core principles
- Design tokens are reusable values (colors, sizes, fonts) captured as variables; they scale design decisions and ensure consistency across platforms.
- Tokens should be named by role (primary-color, spacing-unit) not by visual property (dark-blue, size-16) — role-based names remain valid when themes change.
- Token hierarchies (global, component, state) let you scale changes; changing global spacing affects all components downstream, avoiding scattered hardcoded values.
- Tokens live in a shared source (Design Tokens Community Group format: JSON) that is versioned, reviewed, and consumed by design tools, code, and documentation.
- Token naming conventions vary (BEM, ITCSS, atomic design) — choose one and document it; consistency across teams matters more than the specific system.

## Apex practices
- Version tokens alongside design system; changes to core tokens require major version bumps if they break downstream consumption.
- Implement tokens in both Figma (variables, typography styles) and code (CSS, SCSS, or design system package) — keep sources in sync.
- Document token usage and exceptions; a no-exceptions policy is too rigid, but every exception should be justified and tracked.
- Validate tokens in CI: lint new PR changes against token requirements to catch drift.

## Pitfalls
- Too many token layers causing confusion (global, component, state, variant, modifier) — keep it simple.
- Tokens named by visual property (blue-100) that break when redesigning; migrate to role-based (primary-surface) instead.
- Tokens in Figma but not in code, or vice versa — creates sync issues and confusion.

## Tools & references
Design Tokens Community Group, Figma variables, Style Dictionary (Adobe), Token Studio (Figma plugin), Storybook for token documentation; "Design Systems" (Frostenson & Barker).
