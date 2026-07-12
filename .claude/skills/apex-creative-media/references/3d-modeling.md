# 3D Modeling

## Scope
Creating geometry and structure in three-dimensional space for visualization, animation, games, and fabrication: topology, modeling workflows, and polycount awareness.

## Core principles
- Topology (edge flow and vertex density) is invisible to the final viewer but critical to animation, deformation, and rendering: a quad-based mesh with flow along muscles and joints deforms believably; random triangles don't.
- Polycount is a real constraint (games, real-time rendering, VR) — start low-poly and add detail only where it's visible or serves a purpose; a 10-million-poly model rendered from distance is wasted triangles.
- Modeling is about intention: boolean operations are fast but create terrible topology; modeling by hand (drawing, extruding, connecting) takes longer but produces usable geometry.
- UV mapping (unwrapping 3D geometry to 2D texture space) is as important as the geometry itself; bad UVs cause texture distortion, seams, or wasted texture space.
- The silhouette of the model is what reads first; interior detail doesn't matter if the outline is unconvincing. Build-to-silhouette is a priority.

## Apex practices
- Model from orthographic reference (front, side, top views) before sculpting; ortho-based modeling is controllable and builds proper proportions.
- Use modifiers (subdivision, boolean, array) non-destructively until you commit geometry — non-destructive workflows prevent trapping yourself.
- Check topology as you go by looking at wireframe and edge flow; it's harder to fix after sculpting or subdivision.
- Unwrap UVs with minimal stretching using autounwrap as a start, then manual seam placement to hide them along hard edges (creases, silhouettes).

## Pitfalls
- Modeling too high-poly early (sculpting before establishing basic shape correctly) — start simple, iterate shape, then add detail.
- Ignoring real-time rendering constraints; a perfect offline render won't run in-engine.
- UV seams visible on the final render due to poor seam placement or stretching.

## Tools & references
Blender (free, full-featured), Maya/3DS Max (industry standard for VFX), ZBrush (sculpting), Substance Painter (texturing/baking), Polycount forums (optimization techniques), Ton Roosendaal's modeling principles.
