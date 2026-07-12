# Mobile Testing

## Scope
Testing strategies for mobile apps: unit tests, UI tests, device labs, and beta testing.

## Core principles
- Unit tests (30% of tests by count) are fast and deterministic; test business logic, not UI — mock networking and platform dependencies.
- UI tests (5–10% by count) simulate user interactions; they're slow (seconds per test) and flaky (timing, async, UI state) — keep them minimal and focus on critical flows.
- Integration tests (20–30%) test multiple layers (ViewModel + Repository + Networking) in isolation; faster than UI tests, more realistic than unit tests.
- Device testing (real or emulated) catches platform-specific bugs; emulators are fast but imperfect (no sensors, simulated graphics, different performance).
- Beta testing (closed and open) with real users on real devices catches edge cases and regional issues before app store launch.

## Apex practices
- Aim for 70–80% unit test coverage; write tests for business logic, edge cases, and error paths (retry, offline, invalid data).
- UI tests: focus on critical user journeys (login, purchase, main feature), not exhaustive coverage.
- Use test fixtures and factories to set up test data; avoid brittle hardcoded values.
- Test with various network conditions (fast, slow, offline) and device configurations (memory, screen size, OS version).

## Pitfalls
- Writing UI tests for every screen; they're slow and break on UI changes — focus on critical paths.
- Ignoring flakiness; UI tests that fail intermittently are useless — use explicit waits and avoid hardcoded sleeps.
- Testing only on the latest OS version; test on minimum supported OS to catch compatibility issues.

## Tools & references
XCTest / XCUITest (iOS), Espresso / UIAutomator (Android), Detox (cross-platform), BrowserStack / LambdaTest (device clouds), TestFlight / Google Play Beta; Mockito, OkHttp MockWebServer for mocking.
