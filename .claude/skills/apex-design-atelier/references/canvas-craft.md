# Canvas Craft (Coding the Living Canvas)

## Scope
Creating and updating drawn surfaces in code — Canvas2D/SVG/WebGL, the render loop, immediate vs retained mode — coding like you're crafting reality itself.

## Core principles
- Two worldviews: immediate mode (Canvas2D/WebGL — you repaint the world every frame; the canvas remembers nothing) vs retained mode (SVG/DOM — a scene graph persists and you mutate it). Choose by cardinality and interactivity: thousands of moving particles → immediate; hundreds of clickable, styleable, accessible shapes → retained.
- The render loop is a simulation heartbeat: `update(state, dt) → draw(state)` — state strictly separated from drawing, time passed as delta so motion is frame-rate independent. Every glitchy animation traces back to violating one of these.
- The canvas is resolution-virtual: device pixels ≠ CSS pixels (devicePixelRatio); scale the backing store or ship blur. Coordinate systems are yours to define — model space → world transform → screen is the sane pipeline, and transforms (translate/rotate/scale) beat trigonometry in your object code.
- Redraw economically: clear-and-redraw-everything is correct first; then dirty rectangles, layered canvases (static background / dynamic foreground), and offscreen pre-rendering are the optimization ladder — in that order, measured.
- Determinism is a superpower: same seed, same output — seeded randomness makes generative work reproducible, testable, and versionable (the difference between an artwork and an accident).

## Apex practices
- Structure every sketch as `setup / update / draw` with a single state object — portable across p5, raw canvas, and game engines, and trivially pausable/serializable.
- Use requestAnimationFrame, accumulate dt, and cap it (spiral-of-death guard after tab-sleep); pause the loop when the tab hides.
- Prototype the math at low fidelity first: dots and lines until the motion/layout logic is right; skin it after (the photorealism lesson: values before detail).
- Layer like a painter: background wash → midground forms → foreground accents → glaze (globalAlpha/composite modes); `globalCompositeOperation` is your blend-mode paintbox.

## Pitfalls
- Animating with position += fixed increments (speed varies with refresh rate) instead of dt-scaled velocity.
- One mega-canvas redrawing static content 60×/second — the fans-spinning special.
- Ignoring accessibility: pure-canvas UI is invisible to assistive tech; pair with DOM/ARIA fallbacks or choose SVG when semantics matter.

## Tools & references
MDN Canvas/SVG guides, "The Nature of Code" (Shiffman), p5.js, d3 (retained-mode data joins), WebGL fundamentals (webglfundamentals.org).
