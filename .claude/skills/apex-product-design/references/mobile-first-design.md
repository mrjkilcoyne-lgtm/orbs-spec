# Mobile-First Design

## Scope
Designing for mobile constraints: small screens, touch interaction, responsive design, and performance.

## Core principles
- Mobile-first design starts with small screens and adds features for larger screens (responsive), not the reverse — forces prioritization and clarity.
- Small screens demand simplification: if a feature doesn't fit mobile, it's probably unnecessary — this drives focused design.
- Touch targets must be ≥44x44 pt (iOS) or ≥48 dp (Android) — fingers are less precise than mouse cursors; clustering buttons too tightly causes misses.
- Responsive design (flexible grids, scalable images, media queries) adapts layout to screen size — test on real devices, not just browser resizing.
- Performance matters more on mobile (slower networks, older CPUs); a 5 MB page on desktop is acceptable, on mobile it's torture.

## Apex practices
- Design in a mobile browser first (Chrome DevTools device mode); then tablet, then desktop.
- Use responsive patterns (single-column layout, stacked cards, full-width components) that work across sizes without breakpoint-specific hacks.
- Test navigation on mobile: small screens mean menu buttons, accordions, or bottom navigation (not desktop hamburger menus).
- Optimize images: use srcset and Picture elements for device-appropriate sizes; a 4K photo on mobile is wasted bandwidth.

## Pitfalls
- Desktop-first design that "adapts" to mobile by shrinking text and cramming content (broken mobile UX).
- Assuming responsive = mobile-friendly; responsive can still have small touch targets, slow performance, or bad mobile navigation.
- Ignoring mobile gestures and expecting desktop interactions; swipe-to-delete is mobile idiom, not available on desktop.

## Tools & references
Chrome DevTools mobile emulation, Responsive Design Testing, iOS HIG and Android Material Design for platform patterns, mobile performance audits (Lighthouse).
