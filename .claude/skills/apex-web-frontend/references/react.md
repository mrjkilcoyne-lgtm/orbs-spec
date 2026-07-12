# React

## Scope
Component model, hooks, rendering behavior, and the modern React ecosystem (18/19+).

## Core principles
- UI is a function of state: render is a pure calculation; side effects belong in event handlers first, effects last.
- State is snapshot-per-render; closures capture the render they were born in — most "stale value" bugs are this.
- Reconciliation is identity-based: stable keys, stable component types; defining components inside components remounts them.
- Effects synchronize with external systems; if no external system is involved, you probably don't need one (derive during render instead).
- Lift state to the lowest common owner; colocate everything else.

## Apex practices
- Server components/frameworks (Next/Remix) for data-heavy apps; fetch on the server, interactivity islands on the client.
- Memoize by measuring (React DevTools profiler), not by habit; fix render-cascade causes before wrapping everything in useMemo.
- Custom hooks to package behavior (useThing) — the reuse unit that keeps components declarative.
- Use reducers/state machines for multi-field state transitions instead of five interacting useStates.

## Pitfalls
- useEffect for data transformation/chained state updates (render-time derivation was the answer).
- Missing/wrong dependency arrays silencing the linter instead of restructuring.
- Index-as-key on reorderable lists corrupting input state.

## Tools & references
react.dev (the new docs are excellent), React DevTools profiler, TanStack Query, testing-library.
