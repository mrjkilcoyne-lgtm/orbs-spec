# Mobile Security

## Scope
Protecting app data: local storage, encryption, certificate pinning, authentication, and mobile-specific attack vectors.

## Core principles
- Keychain (iOS) and Keystore (Android) are secure credential storage — use them for tokens, passwords, and secrets, not UserDefaults/SharedPreferences (which are readable by other apps if not encrypted).
- HTTPS with certificate validation is baseline; certificate pinning (hardcoding expected certificate hash) prevents MITM by compromised CAs, but breaks updates if certs rotate without coordination.
- Data at rest should be encrypted: iOS default with iOS 8+ file protection handles this, but ensure sensitive fields use encryption; Android requires explicitly enabling encryption.
- Session tokens expire; refresh tokens are long-lived and exchanged for new access tokens — implement token refresh logic and handle 401/invalidation.
- Jailbreak/root detection is optional (attackers can bypass it), but can block obvious compromises; more important is secure coding practices.

## Apex practices
- Store secrets (API keys, tokens) in Keychain/Keystore, not in hardcoded strings or config files.
- Implement certificate pinning only for APIs you control; use a library (TrustKit for iOS, Network Security Configuration for Android) rather than manual validation.
- Validate server certificates with URLSession (iOS) or HttpsURLConnection (Android) — don't disable certificate validation or accept all certs.
- Implement token refresh: on 401, call refresh endpoint, store new token, retry the request.

## Pitfalls
- Logging sensitive data (tokens, PII); CI logs are often readable — sanitize logs in production builds.
- Storing secrets in source control; use environment variables or secure vaults (Secrets Manager, Vault).
- Certificate pinning with no fallback; if pins are wrong, the app is bricked — test pin updates before rolling out to production.

## Tools & references
iOS Keychain, Android Keystore, TrustKit, OWASP Mobile Security, certificate pinning best practices; security testing with MitmProxy or Charles Proxy.
