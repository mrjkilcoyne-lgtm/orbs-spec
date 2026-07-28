# Layering & Depth

## Scope
Layer, fold, blend, palimpsest: constructing images and interfaces as stacked, interacting strata — from oil glazes to z-index.

## Core principles
- Layering is meaning-construction, not just assembly: each stratum comments on the ones beneath (the palimpsest — old text ghosting through new — turns history into texture). A design with visible strata tells time; a flat design tells only now.
- Painters' depth grammar predates Photoshop: underpainting (structure) → body color (form) → glazes (translucent color shifting what's below) → scumbles (opaque haze) → impasto accents (highest light, thickest paint). Digital layers with blend modes are this exact stack, renamed.
- Depth cues are rankable and mixable: occlusion (strongest), size gradient, vertical position, atmospheric haze (contrast/saturation falloff), blur, parallax, shadow. Interfaces need only two or three, used consistently — Material's elevation system is just occlusion + shadow, ruthlessly systematized.
- The fold is layering in physical space: folding brings distant parts into contact (the map, the brochure, the folded screen) — sequence and surprise from one surface. Digitally: accordions, page transitions, and reveal patterns are folds; what touches what when folded is the design decision.
- Transparency is relational: a translucent layer has no fixed color — it's a function applied to whatever passes beneath (Albers's film color). Design translucent elements against their worst-case background, not their favorite one.

## Apex practices
- Build images back-to-front with named layers and a purpose per layer (structure/form/atmosphere/accent) — if a layer has no describable job, flatten it into another.
- Learn the blend-mode families by what they do to light: multiply darkens (shadow, ink), screen lightens (glow, atmosphere), overlay adds contrast (drama), color/luminosity separate hue from value — pick by intent, not by scrolling the menu.
- Use ghosting deliberately: previous states at low opacity (onion-skinning, edit history, undo previews) — the palimpsest as UX pattern for showing change.
- Establish a depth budget in interfaces: enumerate your elevation levels (e.g., surface/raised/overlay/modal), map shadows and z-index to them once, and forbid freelance z-index values.

## Pitfalls
- Depth soup: mixed cues contradicting each other (big blurry element with a sharp small one in front) — the eye can't build the space.
- z-index arms race (9999) instead of a stacking-context model.
- Transparency stacking until nothing has a color: three 50% layers deep, every hue is mud.

## Tools & references
Oil glazing technique guides, Albers "Interaction of Color" (film color), Material Design elevation spec, Photoshop/Figma blend-mode references, onion-skinning in animation tools.
