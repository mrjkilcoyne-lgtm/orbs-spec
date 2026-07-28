# Wearables

## Scope
Developing for wearable devices: watchOS, Wear OS, battery optimization, input constraints, and always-on displays.

## Core principles
- Wearable screens are tiny (1–2 inches) and have extreme power constraints; aggressive optimization is non-negotiable, not optional.
- Always-on displays (Wear OS, watchOS always-on) burn power even when not interacting; designs must minimize pixel churn and use muted colors for OLED efficiency.
- Input is limited: touchscreen, crown (iOS), buttons — voice input is common; avoid multi-finger gestures or fine motor control.
- Network is often unavailable or metered; wearables sync with phones for internet — assume offline and cascade to phone requests if needed.
- Battery life target is 1–2 days; apps exceeding this are removed or disabled by users — measure with native profilers (Xcode, Android Profiler).

## Apex practices
- Design watch UIs around glances (quick info) and complications (watch face widgets); full-screen apps are rare and power-hungry.
- Use transient notifications for watch apps; they auto-dismiss and don't require action.
- Sync data from phone to watch opportunistically (periodic, on app launch); avoid constant syncing.
- Test always-on mode: disable screen backlight and observe jank; glitchy always-on is unusable.

## Pitfalls
- Full-featured iOS/Android apps shrunk to watch size; useless. Simplify the feature set to glances and one key action.
- Ignoring battery constraints; a watch app that burns 5% battery per hour is deleted immediately.
- Background tasks that run on wearable independently of phone; use phone as the "brain" and watch as the display.

## Tools & references
WatchKit (iOS), Wear OS (Android), Xcode for watchOS, Android Studio for Wear OS; Always-On display optimization guides; Apple Human Interface Guidelines for watchOS; "Building Apps for the Apple Watch" (Ramond-Bates).
