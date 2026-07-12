# Bundlers & Frontend Tooling

## Scope
Vite/webpack/esbuild/Rollup and friends: module graphs, transforms, code splitting, dev servers.

## Core principles
- A bundler is a module-graph compiler: resolve → transform → chunk → emit; every config option hangs off one of these phases.
- Dev and prod are different problems: instant feedback (native ESM, esbuild pre-bundling) vs optimal output (tree-shaking, minification) — modern tools (Vite) split them deliberately.
- Tree-shaking needs ESM and honesty: side-effect-free modules (sideEffects flag), no dynamic require patterns.
- Code splitting follows user journeys: split by route, prefetch by intent; a hundred tiny chunks can be worse than five good ones.
- Hashed filenames + immutable cache headers is the asset caching contract; HTML is the only non-cacheable entry.

## Apex practices
- Analyze before optimizing: bundle visualizers reveal the duplicate lodash, the accidental moment locales, the barrel-file import explosion.
- Set size budgets in CI; fail the build on regression rather than discovering it in Lighthouse.
- Keep config minimal and standard: every custom loader/plugin is future migration pain.
- Understand your transpilation targets (browserslist) — shipping ES5 to evergreen browsers doubles size for nothing.

## Pitfalls
- Barrel files (index.ts re-exporting everything) defeating tree-shaking and slowing dev servers.
- Polyfilling globally what only one dependency needed.
- Different behavior dev vs prod discovered in production (test the built output too).

## Tools & references
Vite docs, esbuild/Rollup docs, bundle analyzers (rollup-plugin-visualizer, statoscope), browserslist.
