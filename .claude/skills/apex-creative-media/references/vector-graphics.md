# Vector Graphics

## Scope
Scalable graphics using paths, shapes, and bezier curves: clean lines, fills, strokes, and precision design that scales from icon to billboard.

## Core principles
- Vectors are mathematical: a circle is defined by center and radius, not pixels; scaling doesn't degrade quality because the shape is recalculated at any size.
- Bezier curves (control points defining curved paths) are the fundamental tool; understanding handles (directional controls on curve) makes smooth, intentional shapes possible.
- Strokes (outlines) and fills (interior color) are separate; a rounded stroke (round-cap, round-join) looks different from a sharp stroke; this matters for logos and icons.
- Layers and groups organize complexity; a logo with 50 shapes is navigable if grouped by component.
- Scalability is the strength but also the constraint: vector graphics work best with bold shapes, clear fills, and limited detail; photorealistic vector is painful.

## Apex practices
- Start with a grid and basic shapes (circles, rectangles, polygons) and combine them (union, subtract, intersect) to create complex forms quickly.
- Use anchor points intentionally: fewer points means smoother curves and smaller file sizes; only add points where curves change direction.
- Create symbol/component systems for logos with variation (horizontal, vertical, icon-only) so you update once and all variations update.
- Export in multiple formats: SVG (web, scalable), PNG (raster fallback), PDF (print), EPS (legacy compatibility) — format choice depends on use case.

## Pitfalls
- Over-complex shapes with too many anchor points; simplify and use strokes/effects instead.
- Assuming vector is "cleaner" than raster; they're different tools for different jobs.
- Ignoring stroke weight scaling: a 2pt stroke scales with the shape, sometimes becoming too thick or thin at different sizes.

## Tools & references
Adobe Illustrator (industry standard, $$), Affinity Designer (one-time purchase alternative), Inkscape (free, open-source), FontForge (font design), SVG spec (web vectors).
