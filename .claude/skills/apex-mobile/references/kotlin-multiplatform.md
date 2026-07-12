# Kotlin Multiplatform

## Scope
Sharing code across platforms using Kotlin: expect/actual declarations, platform-specific implementations, and common code patterns.

## Core principles
- Kotlin Multiplatform (KMP) allows shared code (business logic, API clients) in Kotlin, with platform-specific implementations (iOS/Android UI) — reduces duplication and unifies business logic.
- expect/actual declarations define an interface (expect) and provide platform implementations (actual) — used for platform-specific APIs (file I/O, networking, sensors).
- Common code runs on both iOS (via Kotlin/Native) and Android (via Kotlin/JVM); platform-specific code is isolated and small.
- Coroutines and Flow are multiplatform; the same async patterns work on iOS and Android, simplifying concurrency.
- Binary compatibility: KMP generates frameworks (iOS) and JARs (Android); version changes can break compatibility — versioning is critical.

## Apex practices
- Start with business logic and networking in common code; UI and platform-specific features (sensors, permissions) stay platform-specific.
- Use expect/actual for logging, analytics, and OS-level APIs; implement once per platform, reuse everywhere.
- Test common code with Kotlin multiplatform test framework; unit tests run on all platforms simultaneously.
- Monitor binary compatibility with kotlinx-binary-compatibility-validator; breaking changes require major version bumps.

## Pitfalls
- Attempting to put too much UI logic in common code; platforms have different paradigms (SwiftUI vs Compose) — unify business logic, not UI.
- Ignoring platform differences in concurrency (iOS memory constraints, Android ANR timeouts) — test on real devices.
- Binary instability: changing public API in common code breaks iOS frameworks; use binary compatibility validator in CI.

## Tools & references
Kotlin Multiplatform Mobile (KMM) docs, kotlinx-coroutines, Ktor client, SQLDelight for multiplatform databases; Touchlab KMP workshops; "Kotlin in Action" (Jemerov & Isakova).
