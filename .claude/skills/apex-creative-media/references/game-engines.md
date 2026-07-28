# Game Engines

## Scope
Real-time 3D platforms: rendering, physics, audio integration, scripting, and asset pipelines for shipping interactive experiences across devices.

## Core principles
- The game engine is a runtime that renders pixels, simulates physics, runs scripts, and manages memory — what's possible is defined by its capabilities, not your imagination; choosing the right engine limits or enables your design.
- Frame rate is constant (60 FPS or 120 FPS targets); every frame must complete in 16ms or 8ms respectively, so optimization is not optional (profiling, batching, LOD).
- Physics engines are approximations, not truth; they solve differential equations at 60 Hz so collisions and motion look right, but they can surprise you (stacking, tunneling, ragdoll weirdness).
- Scripting (C#, C++, visual scripting) defines behavior; the engine provides the canvas, but gameplay is code.
- Rendering pipeline (vertex shaders, fragment shaders, post-processing) transforms geometry and textures into pixels; understanding the pipeline makes performance issues solvable.

## Apex practices
- Choose the engine based on your target (PC/console = Unreal/Unity, web = Babylon/Three.js, mobile = Unity, VR = Unreal/Meta Horizon OS SDK); every engine has a native platform.
- Profile from the start (Unity Profiler, Unreal Insights): frame timing, memory, draw calls are visible metrics that guide optimization, not guessing.
- Use prefabs/blueprints for reusable game objects; spawning 1000 unique actors is slower than spawning 1000 instances of the same prefab.
- Iterate on a shipped feature on a real device; editor performance is not device performance (VR is especially unforgiving).

## Pitfalls
- Chasing graphical fidelity at the cost of frame rate — gameplay smoothness is more important than visual polish.
- Loading assets at runtime in gameplay (streaming required) instead of pre-loading in menus.
- Physics on every object; use simple colliders for gameplay, complex geometry only for rendering.

## Tools & references
Unity (industry standard, 2D/3D, mobile), Unreal Engine 5 (AAA graphics, C++), Godot (open-source, lightweight), Babylon.js/Three.js (web), engine-specific profiling tools, GDC talks on optimization.
