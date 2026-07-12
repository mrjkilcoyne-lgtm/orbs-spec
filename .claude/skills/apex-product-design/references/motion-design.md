# Motion Design

## Scope
Animation and transitions: easing curves, duration, choreography, and performance impact.

## Core principles
- Motion has purpose: guide attention (highlight important change), provide feedback (confirm interaction), or create delight — purposeless motion is distracting.
- Easing (acceleration curves) affects perceived smoothness; linear motion feels mechanical, ease-out (deceleration) feels natural, ease-in-out feels springy.
- Duration (100–300 ms for UI micro-interactions, 500 ms–2 s for transitions) should match action complexity; snappy is fun, slow is boring.
- Choreography (multiple animations coordinated) creates flow; all animations at once is chaotic, staggered starts guide the eye.
- Performance matters: 60 FPS (16 ms per frame) is smooth, dropped frames are jank — optimize animated properties (use transform, opacity, not layout changes).

## Apex practices
- Use easing functions from design libraries: ease-out for important transitions, ease-in-out for continuous motion.
- Test animations on real devices (not just high-end); animations that are smooth on desktop can be jank on older phones.
- Respect prefers-reduced-motion (accessibility); offer a non-animated version for users sensitive to motion.
- Prototype animations before building; Figma, Principle, or video prototypes are faster than code for exploring animation direction.

## Pitfalls
- Animating layout properties (width, height, position) causes expensive reflows; use transform (translate, scale) or opacity instead.
- Animations that disable interactions while running; let users interact with an animation in progress.
- Over-animating; a page with 10+ simultaneous animations is overwhelming.

## Tools & references
Easing.net, Principle, Framer, WebAnimation APIs (CSS animations, requestAnimationFrame), Lottie for complex animations; "Animation at Work" (Boulton); performance profiling with DevTools.
