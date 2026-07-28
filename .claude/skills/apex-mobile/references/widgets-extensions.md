# Widgets & Extensions

## Scope
App extensions: home screen widgets (iOS), app widgets (Android), today extensions, watch apps, and other OS-provided extension points.

## Core principles
- Widgets are mini-apps shown on home screen or lock screen; they're powered by your app but run in a sandbox with memory/time limits (iOS ~30 MB, 10 seconds execution).
- Widget updates are scheduled by the OS, not on-demand; request refresh intervals, and the OS decides if/when to grant them — don't assume hourly updates are honored.
- Shared data between app and widget: use App Groups (iOS) or shared SharedPreferences (Android) for synced state; direct database access isn't available to widgets.
- Today extensions (iOS) are legacy; WidgetKit (iOS 14+) is the modern approach — WidgetKit uses SwiftUI and is more efficient than legacy widgets.
- Watch apps (watchOS, Wear OS) have extreme constraints: small screens, limited CPU/battery — designs must be radically simplified.

## Apex practices
- Keep widget logic simple: avoid network requests (use background sync in the app); display cached data with a last-updated timestamp.
- Use push notifications to trigger widget updates (requestPushNotification API); more reliable than polling.
- Test widgets with various states: loading, empty, error; ensure layout works on small screens.
- Watch apps should use complications (small visualizations shown on watch face); they're more engaging than full watch apps.

## Pitfalls
- Widgets that make network requests on every update; they'll drain battery and get killed by the OS for overuse.
- Forgetting to update widgets when app data changes; sync SharedPreferences/App Groups and request widget refresh.
- Over-complex widget UI; small screens mean simple layouts; avoid text-heavy widgets.

## Tools & references
WidgetKit (iOS), AppWidget framework (Android), App Groups / SharedPreferences, WatchKit (iOS), Wear OS apps; Apple WidgetKit tutorials, Android app widget docs; testing with widget simulator.
