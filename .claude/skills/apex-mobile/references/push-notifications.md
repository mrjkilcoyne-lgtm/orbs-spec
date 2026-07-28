# Push Notifications

## Scope
Delivering messages to apps: APNs (Apple), FCM (Google), delivery guarantees, deep integration, and user privacy.

## Core principles
- APNs (Apple Push Notification service) and FCM (Firebase Cloud Messaging) are different networks with different delivery guarantees; APNs is more reliable for user-facing notifications, FCM is flexible but less guaranteed.
- Delivery is at-most-once for both: the server sends a notification, the platform delivers it if the device is online, or drops it after TTL — no retry guarantee, so critical alerts need application-level ACKs.
- Device tokens are per-app per-device per-OS; rotating tokens (re-issued after app updates, device reboots) requires updating your server DB or tokens become stale.
- APNs uses certificates or key-based auth; each certificate expires annually — rotate before expiry or certificates stop working silently.
- FCM supports data messages (handled by app code) and notification messages (handled by platform) — data messages are reliable but need app in foreground; notification messages work in background but are less flexible.

## Apex practices
- Implement notification handling for multiple states: app in foreground (show banner), app in background (system notification), app killed (system notification + deep link on tap).
- Deep link on notification tap to navigate to relevant content — but handle app startup (user launched app normally vs tapped notification).
- Monitor delivery with server-side logging and client-side feedback: have the app ACK receipt to the server for critical notifications.
- Test APNs with a development certificate and test devices; production certificate is needed for app store builds.

## Pitfalls
- Expired APNs certificates silently stop sending — calendar alerts, automated monitoring.
- Assuming delivery means the user will see it; Do Not Disturb, notification settings, or user dismissal means delivery != engagement.
- Sending notifications for every server event (e.g., typing indicators) — batch events and respect user preferences to avoid notification fatigue.

## Tools & references
Apple Push Notification service (APNs) documentation, Firebase Cloud Messaging (FCM), APNs device token handling, Firebase Console for FCM testing; Postman for APNs testing.
