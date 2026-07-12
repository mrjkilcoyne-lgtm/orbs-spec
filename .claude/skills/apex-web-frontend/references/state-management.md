# Frontend State Management

## Scope
Organizing client state: local vs shared, server cache vs UI state, stores and machines.

## Core principles
- Classify first: server cache (someone else's data), UI state (yours, ephemeral), URL state (shareable), form state — each has a right home and wrong homes.
- Server data belongs in a query cache (staleness, refetch, invalidation), not hand-rolled in a global store.
- Derive, don't duplicate: every copy of a fact is a future inconsistency; compute from the minimal source set.
- Single direction of data flow keeps causality traceable: state → view → action → state.
- The URL is state management: filters, tabs, selection that users expect to share/bookmark/back-button.

## Apex practices
- Reach for global stores only for genuinely cross-cutting client state (session, theme, cart) — most "global state" is server cache in disguise.
- Model complex interactions as explicit state machines/statecharts; impossible states become unrepresentable.
- Keep state minimal and normalized (byId + ids) when entities interrelate; selectors compute views.
- Persist deliberately (what, where, for how long, migration on shape change), not by dumping the store to localStorage.

## Pitfalls
- Mirror-state: copying props/query results into local state and watching them drift.
- One giant store where every widget subscribes to everything (render storms).
- Boolean flag combinatorics (isLoading && !isError && isFetched) instead of a status enum.

## Tools & references
TanStack Query/SWR, Zustand/Redux Toolkit, XState, URL state helpers (nuqs).
