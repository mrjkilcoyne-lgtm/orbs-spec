# Geolocation

## Scope
Location services: GPS accuracy, privacy permissions, background tracking, and location-based features.

## Core principles
- GPS accuracy varies: outdoor clear sky is ~5 m, urban canyons are 10–50 m, indoors is 20+ m or unavailable — design features around accuracy, not ideal cases.
- Location permissions are separate for foreground (CLLocationManager.requestWhenInUseAuthorization) and background (requestAlwaysAndWhenInUseAuthorization); users understand background location sharing is a privacy risk.
- Location updates drain battery significantly; batch updates (e.g., every 60 seconds) and stop when background to minimize drain.
- Privacy: never track location without explicit user consent; minimally required location data only; Apple's App Privacy labels (Privacy Manifest) must disclose location usage.
- Geofencing (CLCircularRegion) lets the OS detect entry/exit without constant polling — more efficient than constant location updates.

## Apex practices
- Request permissions with clarity: show why location is needed before requesting (permission-with-context).
- Use `pausesLocationUpdatesAutomatically = true` to let the OS pause updates when the user isn't moving, saving battery.
- Batch location updates: don't update UI on every GPS sample; accumulate updates and process every 10–30 seconds.
- Test with location simulation in Xcode/Android Emulator; vary accuracy (set desiredAccuracy) to handle urban/indoor scenarios.

## Pitfalls
- Always requesting "Allow Always" (background location); disclose the use case and make foreground-only the default.
- Assuming GPS is always available; have fallback (cell tower triangulation, IP geolocation) or graceful degradation.
- Leaving location updates running when app goes background without needing them; apps that track location unnecessarily get flagged by app reviewers.

## Tools & references
Core Location (iOS), LocationManager (Android), CLCircularRegion, significant location change; Privacy Manifest (iOS); geofencing APIs; test location spoofing with emulators.
