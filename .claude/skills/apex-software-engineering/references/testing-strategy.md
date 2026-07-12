# Testing Strategy

## Scope
Deciding what to test, at which layer, and with what fidelity — the portfolio, not individual tests.

## Core principles
- Tests exist to enable change: optimize for confidence per maintenance cost.
- Test behavior through public interfaces, not implementation details; refactors shouldn't break tests.
- The pyramid is a heuristic: many fast unit tests, fewer integration, few end-to-end — but integration tests often carry the most real confidence.
- Every test answers: what breakage would this catch that nothing else does?
- Flaky tests are worse than no tests; they train people to ignore red.

## Apex practices
- Write one high-fidelity happy-path test per feature plus targeted edge-case units.
- Use test doubles for the process boundary, real implementations inside it.
- Make tests deterministic: control time, randomness, and network explicitly.
- Track escaped defects and add the missing test layer, not just the missing test.

## Pitfalls
- 100% coverage of getters while the money path is untested.
- Mocking so heavily the test asserts the mock, not the system.
- End-to-end suites so slow nobody runs them before merging.

## Tools & references
"Software Engineering at Google" testing chapters, property-based testing (Hypothesis, QuickCheck), mutation testing.
