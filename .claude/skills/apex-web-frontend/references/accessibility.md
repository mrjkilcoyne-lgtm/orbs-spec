# Web Accessibility (a11y)

## Scope
Building interfaces usable by people with visual, motor, auditory, and cognitive disabilities — WCAG as floor, usability as goal.

## Core principles
- Accessibility is a quality attribute, not a feature: cheapest at design time, most expensive as retrofit.
- POUR: perceivable, operable, understandable, robust — every WCAG criterion hangs off these.
- Keyboard is the litmus test: everything reachable, visible focus, logical order, no traps.
- The accessibility tree is your real output: names, roles, states — inspect it like you inspect the DOM.
- Color contrast (4.5:1 body text) and never color alone to convey meaning.

## Apex practices
- Semantic HTML delivers 80%; ARIA fills gaps following the ARIA Authoring Practices patterns (and their keyboard contracts).
- Manage focus deliberately in SPAs: route changes announce, modals trap and restore.
- Automated checks (axe) catch ~30-40%; manual keyboard + screen reader passes (NVDA/VoiceOver) catch the rest.
- Test with real settings: 200% zoom, reduced motion, high contrast, prefers-color-scheme.

## Pitfalls
- aria-label sprinkled on everything while roles/states are wrong (ARIA making things worse).
- Focus outlines removed for aesthetics with no replacement.
- Announcements missing for async updates (use live regions sparingly and correctly).

## Tools & references
WCAG 2.2, ARIA Authoring Practices Guide, axe-core, WebAIM articles, screen readers themselves.
