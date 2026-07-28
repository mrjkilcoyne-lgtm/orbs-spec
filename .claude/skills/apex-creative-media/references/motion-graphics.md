# Motion Graphics

## Scope
Animating design elements and text: timing, easing, layering, compositing with live action or static backgrounds, and using motion to tell stories or guide attention.

## Core principles
- Animation is about time and spacing: the same arc traveled in 10 frames feels snappy, in 30 frames feels floaty; easing (acceleration/deceleration curves) makes motion feel natural or stylized.
- Layers (depth and stacking) in composition create visual hierarchy; foreground and background motion at different speeds (parallax) creates depth on a 2D surface.
- Motion should have purpose: drawing attention to important information, clarifying a transition, adding emphasis, or enhancing emotion — gratuitous motion distracts.
- Keyframe animation (manual position/rotation/opacity at frame X) is expensive but precise; procedural animation (noise, physics, expressions) scales and looks organic.
- Integration with live action (chroma key, rotoscoping, tracking) requires planning on set and post; mismatched frame rates, lighting, or tracking breaks immersion.

## Apex practices
- Study Disney's 12 principles of animation (squash, stretch, anticipation, overlapping action, arcs) — they apply whether you're moving a ball or text.
- Use expressions (After Effects JavaScript) and plugins (like Plexus, Form) to generate and evolve motion procedurally; it's faster than keyframing repetitive motion.
- Plan composition early (layout, hierarchy, type treatment) so animation enhances it rather than competing; overcomplicated motion on poor design reads as frenetic, not professional.
- Render proxies/precomps to maintain playback performance in editor; real-time feedback is worth the organizational overhead.

## Pitfalls
- Animating everything just because you can; static, moving text, and moving graphics should have a hierarchy of importance.
- Easing everything with ease-in-ease-out (linear motion feels robotic, but so does easing on every frame); restraint shapes perception.
- Ignoring frame rate and temporal coherence; motion should feel smooth and intentional, not jittery.

## Tools & references
After Effects (de facto standard for motion design), Cinema 4D (3D motion, integration), Blender (free, VFX-grade compositing/animation), Adobe's animation principles, Richards' "The Animator's Survival Kit."
