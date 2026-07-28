# Test-Driven Development

## Scope
Red-green-refactor as a design discipline: writing the test before the code it verifies.

## Core principles
- The failing test is the spec; watch it fail for the right reason before making it pass.
- Write the minimum code to pass, then refactor with the green bar as safety net.
- TDD is a design tool: hard-to-write tests reveal coupling before it ships.
- Small cycles (minutes, not hours) keep feedback tight and rollback cheap.
- Not everything warrants TDD: exploratory spikes and UI glue may not — decide, don't drift.

## Apex practices
- Start each feature with a list of test cases; strike through as you go, add as you learn.
- Name tests as behavior statements ("rejects expired token") not method references ("testValidate2").
- When a bug is found, write the failing test first — it proves the fix and prevents regression.
- Refactor tests too: they're production code for your development process.

## Pitfalls
- Green-bar addiction: skipping the refactor step until tests calcify around bad design.
- Writing tests after and calling it TDD — the design benefit is gone.
- Testing implementation sequence (mock call order) instead of outcomes.

## Tools & references
Beck's "Test-Driven Development: By Example," Freeman & Pryce "GOOS," fast watch-mode test runners.
