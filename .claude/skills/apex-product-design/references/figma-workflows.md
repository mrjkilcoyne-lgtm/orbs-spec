# Figma Workflows

## Scope
Designing in Figma: component systems, variants, variables, libraries, and collaborative workflows.

## Core principles
- Components in Figma are reusable design objects; changing a main component updates all instances — this enforces consistency but requires careful component hierarchy design.
- Variants (component states: default, hover, disabled) keep related states in one component; multiplied variants (size × color × state) explode complexity — use sparingly.
- Variables (global, scoped) replace hardcoded values; a color variable can be swapped for dark mode, and all instances update — transforms design iterations from manual to automatic.
- Shared libraries (team files, assets) scale design systems; all projects pull from the library and receive updates — version control matters.
- Auto-layout (flexbox-like constraints) makes responsive design in Figma feasible; components scale to content, gaps adjust, nested auto-layout creates complex layouts.

## Apex practices
- Build component libraries with clear hierarchy (Button > Button Group, Input > Form) and documentation; component names should be self-documenting.
- Test component instances before shipping; variously configured instances should work (small button, large button, with icon, without icon).
- Use Figma Dev Mode and handoff specs (measurements, colors, fonts extracted from design) for developer clarity.
- Implement design tokens as Figma variables; link to colors, typography, spacing so changes propagate across projects.

## Pitfalls
- Components with too many variants (20+ combinations); simplify by removing unnecessary combinations or splitting into smaller components.
- Breaking component instances (detaching to edit locally); instances should be used as-is; if adjustments are common, the component is wrong.
- Unused library components that rot; periodically audit and retire unused components or mark as deprecated.

## Tools & references
Figma components and variables, Figma Dev Mode, FigJam for collaboration, Figma API for integrations; design system templates (Petal, Primer); "Component Driven" (Bayer & Dontcheva).
