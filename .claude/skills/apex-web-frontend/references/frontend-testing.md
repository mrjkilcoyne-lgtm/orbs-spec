# Frontend Testing

## Scope
Testing UI code: component tests, E2E, visual regression, and what to test where.

## Core principles
- Test what the user experiences: query by role/label, assert visible outcomes — the more tests resemble usage, the more confidence (Testing Library's law).
- The frontend trophy: lean E2E for critical journeys, a solid middle of component/integration tests, units for pure logic.
- Flake is the enemy: deterministic waits (auto-retrying assertions, network interception), never sleep(); one flaky suite kills the practice.
- Test behavior contracts, not snapshots of implementation: broad snapshot tests fail on every change and verify nothing.
- Mock at the network boundary (MSW/route interception), keep everything inside the app real.

## Apex practices
- Playwright/Cypress for the 5-10 money paths (signup, checkout, core loop) run on every merge.
- Component tests with Testing Library for states: loading, empty, error, populated, interactive flows.
- Accessibility assertions in tests (axe) and role-based queries doubling as a11y verification.
- Visual regression (Chromatic/Percy) for design-system components where pixels are the contract.

## Pitfalls
- Testing implementation details (state values, instance methods) that break on refactor.
- E2E suites covering everything, taking 40 minutes, trusted by no one.
- data-testid everywhere hiding real accessibility gaps role queries would have caught.

## Tools & references
Testing Library, Playwright, MSW, axe-core, Kent Dodds' Testing Trophy writings.
