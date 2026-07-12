# In-App Purchases

## Scope
Monetizing apps with in-app purchases: transaction handling, receipt validation, entitlements, and fraud prevention.

## Core principles
- App Store (iOS) and Google Play (Android) handle payment processing — the app requests a purchase, the platform shows payment UI, and provides a receipt/token.
- Receipt validation must happen server-side: the app sends the receipt to your backend, which validates it with Apple/Google — don't trust client-reported purchases.
- Subscriptions renew automatically (if not cancelled); your backend must process renewals and manage entitlements, as the client may not be running.
- Sandbox testing allows testing IAP flow without real payments; use sandbox credentials in test builds to avoid accidental charges.
- Restore purchases: iOS requires a "Restore" button allowing users to re-download previous purchases (App Store guideline) — store purchase history server-side and query it on restore.

## Apex practices
- Store purchase receipts and entitlements on your server; check entitlements server-side before granting access (ignore client claims).
- Implement a renewal webhook: App Store and Google Play notify your server of subscription renewals, cancellations, and failures — use this to update server-side entitlements.
- Handle edge cases: network fails after payment but before receipt receipt; use a queue to retry receipt validation and sync state.
- Test with Sandbox credentials for iOS; use internal testing track for Android; never test with real payments.

## Pitfalls
- Trusting the client's receipt without server validation; a jailbroken iOS or modified Android app can fake purchases.
- Assuming subscription renewal == active entitlement; subscription can be cancelled, failed to renew, or expired — check expiry date server-side.
- Forgetting to persist purchase state server-side; if the app is uninstalled and reinstalled, local state is gone, but entitlements should persist (if restoring on login).

## Tools & references
StoreKit 2 (iOS), Google Play Billing Library (Android), App Store Server Notifications, receipt validation APIs; StoreKit docs, RevenueCat for IAP backend; testing with Sandbox/internal testing.
