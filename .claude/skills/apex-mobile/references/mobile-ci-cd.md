# Mobile CI/CD

## Scope
Automated testing, building, signing, and distribution for iOS and Android: CI/CD pipelines, beta testing, and app store submission.

## Core principles
- Mobile CI/CD requires signing (certificates, provisioning profiles for iOS; keystores for Android), which must be kept secret in the CI environment — use encrypted environment variables or secure vaults.
- Beta distribution channels (TestFlight for iOS, Google Play Beta for Android, Firebase App Distribution) allow testing before app store release — required to catch bugs pre-production.
- Automated UI tests (Espresso, XCUITest) run on emulators/simulators in CI; they're slow (minutes per test) and flaky (UI timing), but essential for regression — run subset on each push, full suite nightly.
- Build signing happens in CI; the pipeline must manage certificates (renewal), provisioning profiles (team membership), and signing configuration (which certificate for dev/beta/prod).
- Release trains (beta tags, release branches) prevent confusion; a release is a specific build tagged for a specific app store version.

## Apex practices
- Use fastlane to automate signing, building, and uploading; it handles certificate management and app store API calls — reduces manual steps.
- Separate CI stages: unit tests (seconds), build (minutes), beta upload (minutes), production submission (manual gate).
- Pin tool versions (Xcode, Android SDK, fastlane) in CI configuration; xcode-select or Android Gradle won't auto-update, preventing surprise breaks.
- Test crash logs and analytics: each beta build should push a test crash and verify it reaches your analytics backend.

## Pitfalls
- Signing in CI without proper secrets management; leaked certificates enable unauthorized uploads and ad-hoc signing.
- Over-strict version pinning that prevents security updates; use ranges (Xcode 15.0+) rather than exact versions.
- Running full test suite on every push; prioritize by test time and coverage, run full suite only on release branches.

## Tools & references
fastlane, GitHub Actions / GitLab CI / Jenkins for mobile, TestFlight, Google Play Console, Firebase App Distribution; Apple certificate and provisioning profile docs; Xcode Cloud for iOS CI/CD.
