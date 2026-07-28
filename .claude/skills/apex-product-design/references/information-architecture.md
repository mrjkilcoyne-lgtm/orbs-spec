# Information Architecture

## Scope
Organizing and structuring content and navigation: mental models, hierarchy, labeling, and user findability.

## Core principles
- Information architecture (IA) reflects how users mentally organize information about the domain; if IA doesn't match user mental models, discoverability fails.
- Card sorting (open or closed) reveals how users group content — organizes IA decisions by evidence, not designer opinion.
- Hierarchy depth vs breadth tradeoff: a single level (all items visible) overwhelms; deep nesting (clicking through hierarchies) is slow — usually 3–5 levels is a sweet spot.
- Labeling matters: labels (category names, link text) shape whether users can predict what's behind a link — ambiguous labels cause wrong clicks and backtracking.
- Findability: 80% of users should find a task in 3 clicks or less — deeper structures fail unless signposting (breadcrumbs, trail) shows location.

## Apex practices
- Conduct open card sorting (users group content) before designing navigation, and closed card sorting (users sort into pre-defined buckets) to validate IA.
- Test navigation with users; show them a task and observe if they can complete it — actual behavior beats designer assumptions.
- Use consistent taxonomy across the product; if the same concept is called "Account" on one page and "Profile" on another, users get lost.
- Design breadcrumbs and search as fallback navigation; if IA is clear, users rarely use them, but they're essential for backtracking.

## Pitfalls
- IA that mirrors internal organization (departments, engineering structure) instead of user mental models.
- Over-categorizing: creating too many categories for few items dilutes focus; consolidate related items.
- Ignoring search; if IA is broken, search masks the problem but doesn't fix it — fix IA, then optimize search.

## Tools & references
Card sorting software (Optimal Workshop, UserTesting), tree testing for IA validation, System Usability Scale (SUS), Information Architecture Institute resources; "Designing Web Navigation" (Morville & Rosenfeld).
