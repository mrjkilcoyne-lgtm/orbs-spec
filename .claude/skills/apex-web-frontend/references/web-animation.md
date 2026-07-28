# Web Animation

## Scope
Motion on the web: CSS transitions/animations, WAAPI, scroll-driven effects, and performance.

## Core principles
- Animate compositor properties (transform, opacity) — they skip layout/paint; animating width/top/left janks.
- Motion needs purpose: orientation (where did it go), causality (what triggered what), continuity — decoration is the lowest tier.
- Duration/easing carry the feel: 150-300ms for UI, ease-out for entrances, ease-in for exits; springs for natural interruption.
- prefers-reduced-motion is non-negotiable: provide the reduced path (opacity swaps) for vestibular safety.
- Interruptibility separates good from great: animations driven by state can reverse mid-flight; fire-and-forget ones fight the user.

## Apex practices
- CSS transitions for state changes, WAAPI/libraries for orchestration, FLIP technique for layout animations at compositor cost.
- View Transitions API for page/element transitions instead of manual clone choreography.
- Scroll-driven animations (CSS scroll-timeline) over scroll event listeners.
- Test on a mid-tier Android; DevTools Performance panel confirms 60fps, not your eyes on an M-series.

## Pitfalls
- Animating everything: motion inflation makes interfaces feel slower, not richer.
- Layout thrash from JS animation loops reading and writing layout per frame.
- Infinite/looping motion near text content (distraction, accessibility).

## Tools & references
Motion (Framer Motion), WAAPI on MDN, FLIP (Paul Lewis), View Transitions docs, cubic-bezier.com.
