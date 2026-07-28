# Combination Patterns

## Scope
The stacking grammar: which skillset combinations produce more than the sum of their parts, and how to choose a stack fast.

## Core principles
- Stacks have roles, not just members: every stack needs a DOMAIN lens (subject matter), a CRAFT lens (artifact type), and a CHECK lens (failure finder). Two domain lenses and no check lens is the most common mis-stack — deep expertise, unreviewed.
- Cross-tier combinations are where the magic is: technical × aesthetic (canvas-craft + rothko-color-fields for an ambient dashboard), technical × human (api-design + human-factors for developer experience), business × craft (unit-economics + pricing-strategy + positioning for a pricing page). Same-tier stacks deepen; cross-tier stacks differentiate.
- Three lenses is the ceiling per pass: beyond three, principles start conflicting without a resolution rule and the reader of your stack can't predict your standard. Run multiple passes with different stacks instead of one pass with six lenses.
- Some pairs are standing partnerships — learn them as units: design-atelier + web-frontend (anything visual on the web), blindspots + anything (every review), sagas + idempotency + background-jobs (every async workflow), statistics + ab-testing + product-metrics (every experiment readout), security + trust-boundaries (every input surface).
- The stack is chosen by the artifact's audience, not the builder's comfort: an internal script gets engineering lenses; the same logic as a customer-facing page adds design, human-factors, and i18n lenses — audience determines which failures matter.

## Apex practices
- Write the stack declaration before starting: "Stack: X(area, area) + Y(area) + blindspots(area, area)" — one line, forces the decision, makes the review reproducible.
- Use opposing-lens pairs deliberately for tension: photorealism (maximum fidelity) vs cave-drawing (maximum economy) bracket any fidelity decision; move fast (swarm) vs verify-before-assertion bracket any speed decision. Naming both poles locates your position honestly.
- Keep a combos log: when a stack works (or misses something), record it — the org's combination memory compounds like Ogilvy's swipe file.
- For unfamiliar territory, stack one familiar lens with the unfamiliar domain: the familiar lens gives you footing while the domain reference teaches — never enter new territory lens-naked.

## Pitfalls
- Lens-shopping to justify a done decision (picking the skillset whose principles bless what you already built) — choose the stack before the work.
- Reading whole skillsets instead of the 2-3 relevant area files: the system is designed for surgical loads; bulk loading is token waste and attention blur.
- Forgetting the check lens under deadline pressure — exactly when it pays most.

## Tools & references
The 27 skillset SKILL.md files as the menu; apex-blindspots as the universal check lens; the conductor agent for stacks at swarm scale.
