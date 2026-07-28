# Micro-Frontends

## Scope
Splitting frontend ownership across teams: composition strategies, shared dependencies, when not to.

## Core principles
- Micro-frontends solve an organizational problem (independent team deployment), not a technical one; without the org pain, they're pure overhead.
- Composition choice defines everything: build-time (npm packages), server-side (fragments/edge includes), client-side (module federation) — each trades autonomy against consistency and performance.
- Vertical slices by user journey beat horizontal layers; a team owns a route/domain end-to-end.
- The contract surface must be tiny and versioned: routing, auth/session, design tokens, eventing — everything else stays private.
- Shared runtime dependencies are the tax: duplicate React downloads or coupled upgrade trains — pick your poison explicitly (import maps/federation shared scope).

## Apex practices
- Start with a well-modularized monolith (workspace packages, enforced boundaries); extract to runtime composition only when deploy independence is truly blocked.
- Centralize the shell: one owner for routing, auth, telemetry, error boundaries; fragments fail independently without blanking the page.
- Design-system package as the consistency backbone — visual drift is the first user-visible symptom of MFE rot.
- Contract-test the seams (events, exposed modules) so teams can deploy without cross-team regression fear.

## Pitfalls
- Five frameworks in one page because "autonomy" — users pay the megabytes.
- Shared mutable global state between fragments (hidden coupling that breaks independently-deployed assumptions).
- MFE for a 10-person team: all the complexity, none of the payoff.

## Tools & references
Module Federation docs, single-spa, import maps, "Micro Frontends" (Geers), Martin Fowler's article.
