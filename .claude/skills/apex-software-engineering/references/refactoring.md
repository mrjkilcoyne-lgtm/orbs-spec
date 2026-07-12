# Refactoring

## Scope
Restructuring code without changing observable behavior, in small reversible steps.

## Core principles
- Refactoring requires a safety net: tests (or characterization tests) come first.
- Small steps that keep the build green beat big-bang rewrites; commit at each stable point.
- Separate refactoring commits from behavior-change commits — never mix.
- Code smells (long method, feature envy, shotgun surgery) indicate where, not how.
- The best refactorings reduce coupling or increase cohesion; cosmetic churn is not refactoring.

## Apex practices
- Use automated refactorings (rename, extract, inline) from the IDE — they're proof-preserving.
- Apply "prepare the change, then make the change": refactor until the feature is a one-line diff.
- Strangler-fig larger restructures: route through the new path incrementally.
- Timebox exploratory refactors; revert freely when a direction fails.

## Pitfalls
- Refactoring without tests and calling manual checks "verification."
- Scope creep: a rename that becomes a redesign in one PR.
- Improving code nobody touches while hot paths stay tangled.

## Tools & references
Fowler's "Refactoring" catalog, IDE refactoring engines, Feathers' "Working Effectively with Legacy Code."
