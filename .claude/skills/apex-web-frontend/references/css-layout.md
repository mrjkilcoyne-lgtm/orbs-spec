# CSS Layout

## Scope
Flexbox, Grid, flow layout, positioning, and the cascade as a system.

## Core principles
- Normal flow is the base layer; understand block/inline formatting contexts before overriding them.
- Flexbox for one dimension (distribute along a line), Grid for two (place in an area) — choosing right removes most hacks.
- The box model + `box-sizing: border-box` everywhere; margins collapse in flow, not in flex/grid.
- Specificity wars are self-inflicted: flat selectors, layers (@layer), custom properties for theming.
- Intrinsic sizing (min-content, max-content, fit-content, minmax) lets content drive layout — the modern replacement for magic numbers.

## Apex practices
- Grid template areas for page scaffolds — readable ASCII-art layout that refactors easily.
- Gap over margin-between-siblings; logical properties (margin-inline) for writing-mode resilience.
- Custom properties as design tokens; calc()/clamp() for fluid values.
- Debug with browser DevTools layout inspectors (grid/flex overlays), not trial-and-error.

## Pitfalls
- Absolute positioning as a layout tool (it removes elements from the layout conversation).
- Fixed heights causing overflow; prefer min-height and let content size.
- z-index arms race instead of understanding stacking contexts.

## Tools & references
CSS Grid Garden/Flexbox Froggy, Josh Comeau's CSS course notes, MDN layout guides, every-layout.dev.
