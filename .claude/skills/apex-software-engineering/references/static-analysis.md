# Static Analysis

## Scope
Machine-checking code without running it: linters, type systems, formatters, security scanners.

## Core principles
- Push checks left: an error caught at edit time costs minutes; in production, days.
- Types are the cheapest static analysis — encode units, states, and nullability in them.
- A rule that produces uninspected warnings is worse than no rule; zero-warning policy or delete the rule.
- Formatters end style debates permanently; adopt the standard one and never discuss again.
- Analysis findings are hypotheses; false-positive rates determine whether a tool survives.

## Apex practices
- Enforce in CI as blocking, run locally as instant (editor integration, pre-commit).
- Ratchet on legacy code: forbid new violations without demanding a big-bang cleanup (baseline files).
- Write custom rules for your project's recurring review comments — reviewers shouldn't be linters.
- Treat suppression comments as code review items requiring justification.

## Pitfalls
- Enabling every rule then drowning in noise until the tool is ignored.
- `any`/`unsafe`/`@ts-ignore` sprawl silently disabling the type system.
- Style rules blocking merges while real defect classes go unchecked.

## Tools & references
typed language strict modes, golangci-lint, ruff, ESLint, Semgrep/CodeQL for custom patterns.
