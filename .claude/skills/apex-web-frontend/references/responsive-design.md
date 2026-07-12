# Responsive Design

## Scope
Interfaces that adapt across viewport sizes, input types, and device capabilities.

## Core principles
- Content-out, not device-in: breakpoints where the design breaks, not at iPhone model widths.
- Mobile-first CSS (min-width media queries) forces prioritization and produces lighter base styles.
- Fluid by default: relative units (rem, %, ch), clamp() for type scales, flexible images (max-width: 100%).
- Container queries size components by their container, not the viewport — components become truly portable.
- Responsiveness includes input (touch targets ≥44px, hover as enhancement) and preference (reduced motion, color scheme).

## Apex practices
- Test at arbitrary widths by dragging, not just device presets; the bugs live between breakpoints.
- Use `srcset`/`sizes` and modern formats so mobile doesn't download desktop images.
- Viewport units with care: dvh/svh for mobile browser chrome reality.
- Design the 320px and the ultrawide case explicitly; the middle usually follows.

## Pitfalls
- Hiding content on mobile instead of reprioritizing it — mobile users want the same tasks.
- Fixed-width tables/embeds punching out of the layout.
- Breakpoint spaghetti: dozens of overrides instead of fluid foundations.

## Tools & references
web.dev responsive course, container query guides, utopia.fyi for fluid scales, browser device toolbar.
