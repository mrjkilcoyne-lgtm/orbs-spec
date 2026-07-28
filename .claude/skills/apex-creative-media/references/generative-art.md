# Generative Art

## Scope
Using algorithms and randomness to create artwork: procedural generation, noise, emergence, interactivity, and the aesthetic of deterministic rules producing non-deterministic output.

## Core principles
- A generative system is defined by its inputs (parameters, seeds, initial state) and rules (algorithm, constraints, feedback loops) — it doesn't write its own rules, you do.
- Randomness without constraint is noise; Perlin noise, fractal brownian motion, and other coherent noise create patterns that feel organic because they have internal structure.
- Parameters control the space of possibility: a few well-chosen parameters that affect many outputs (parameter space reduction) are easier to explore than hundreds of independent dials.
- Emergence: simple rules applied recursively can create complex, unexpected forms (Conway's Life, Lindenmayer systems, cellular automata); surprising results come from understanding your rules deeply enough to predict they'll surprise you.
- Iteration and evolution: variations of a seed or small adjustments to parameters can be displayed as a grid (sheet of variations), allowing visual search for interesting states.

## Apex practices
- Start with simple rules (gravity, collision, decay) before complex algorithms; a few local behaviors often create emergent global patterns.
- Seed randomness: a saved seed produces the same output every time, allowing reproduction and curation of generated variations.
- Use parameter animation: animate parameter values over time to see how the system evolves; it's often more interesting than static output.
- Display process, not just result: animation of generation reveals structure and rule-following that static images hide.

## Pitfalls
- Randomness as an excuse for lack of intent: generative art with no aesthetic direction is algorithmic wallpaper.
- Over-parameterization: too many controls make the system hard to explore and predict.
- Ignoring visual craft: even generative art needs composition, color, and refinement; algorithm doesn't excuse ugly output.

## Tools & references
Processing (learning-friendly, visual), p5.js (web-based), Shader Art (GLSL), Houdini (procedural modeling), Perlin noise, genetic algorithms, Whitelaw's "Metacreation," Reas & McWilliams' "Processing: A Programming Handbook."
