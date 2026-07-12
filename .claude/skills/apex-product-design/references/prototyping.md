# Prototyping

## Scope
Interactive mockups: fidelity levels, testing prototypes with users, animation, and moving toward production.

## Core principles
- Fidelity (visual detail) and interactivity are independent: a high-fidelity mockup can be non-interactive (static screens); a low-fidelity interactive prototype (Figma with interactions) tests flows.
- Prototype for the question you're answering: flow validation needs clickable prototypes, visual refinement needs high-fidelity statics, animation needs video/Figma prototype.
- User testing with prototypes is fast and cheap compared to building code; interactive prototypes catch navigation, clarity, and flow problems before development.
- Animation prototypes (Principle, Framer, After Effects) show motion more realistically than Figma; use for micro-interactions and transitions to verify they feel right.
- Hand-off clarity: developers need a single source of truth (design system, component library, specs) to minimize questions and rework.

## Apex practices
- Prototype only the critical path first; don't prototype entire flow if a few screens test the core hypothesis.
- Use Figma prototyping for flows and interactions; it's fast, shareable, and developers can inspect components.
- Test prototypes with target users; ask them to accomplish a task without explaining how (unmoderated testing via UserTesting or Maze).
- Export interactive PDFs or video walk-throughs for stakeholder reviews when Figma sharing isn't feasible.

## Pitfalls
- Over-prototyping: building high-fidelity prototypes for every idea without testing whether the idea is worth building.
- Prototypes that don't represent final interaction model; a Figma overlay interaction is different from native app interaction (latency, responsiveness).
- Prototype polish causing scope creep; people treat beautiful prototypes as "almost done," expecting minimal changes before handoff.

## Tools & references
Figma (prototyping and design), Principle (animation), Framer (code-based), UserTesting / Maze (remote testing), Lookback (moderated testing); "Hooked: How to Build Habit-Forming Products" (Eyal) for testing mental models.
