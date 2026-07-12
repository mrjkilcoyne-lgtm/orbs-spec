# Deep Linking

## Scope
URL-based app navigation: URI schemes, universal links, app links, state restoration, and handling deep links from external sources.

## Core principles
- Deep links are URLs that route to specific app content; `myapp://user/123` (scheme) or `https://myapp.com/user/123` (universal/app links) navigate to user 123.
- URI schemes (myapp://) are fast but not verifiable; any app can claim the same scheme, causing conflicts — use universal links (iOS) or app links (Android) which are verified via DNS.
- Universal links require an apple-app-site-association file on your domain (HTTPS); app links require assetlinks.json on the domain.
- Deep links can arrive in different states: app not running (needs cold start, then navigate), app running in background (navigate), app running in foreground (handle intent/routing).
- State restoration requires saving the deep link path and re-applying it after app launch; without it, cold-started apps show the home screen, not the linked content.

## Apex practices
- Implement a routing layer (Router, Navigation, NavigationStack) that parses deep link URLs and maps them to screens — centralize this to avoid scattered link handling.
- Test deep links with `adb shell am start -a android.intent.action.VIEW -d "myapp://..."` (Android) or `xcrun simctl openurl` (iOS).
- Handle state restoration: save deep link path when app is backgrounded, restore it on foreground if needed.
- Verify DNS configuration for universal/app links (apple-app-site-association, assetlinks.json) using online validators.

## Pitfalls
- Assuming URI schemes work across devices (conflicts with other apps using the same scheme).
- Not handling the case where the linked content doesn't exist (404 on server or deleted); show an error or fallback screen.
- Deep links that require authentication but user isn't logged in; implement pre-authentication deep link handling or SSO.

## Tools & references
Branch.io, Firebase Dynamic Links, apple-app-site-association and assetlinks.json formats, deep link validation tools; platform-specific navigation frameworks (SwiftUI NavigationStack, Android Navigation Compose).
