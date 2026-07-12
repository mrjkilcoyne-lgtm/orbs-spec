# OAuth / OIDC

## Scope
Delegated authorization (OAuth 2.x) and federated authentication (OpenID Connect): flows, token handling, and the modern hardening baseline.

## Core principles
- OAuth is authorization, OIDC is authentication layered on top — using a bare OAuth access token as proof of identity enables token-substitution login bypasses; identity comes from the ID token with validated `iss`, `aud`, `nonce`, and signature.
- Authorization Code + PKCE is the only current-best-practice flow for public clients (SPAs, mobile); the implicit grant and resource-owner password grant are deprecated by the OAuth 2.0 Security BCP (RFC 9700) and OAuth 2.1.
- Exact-match redirect URI validation is load-bearing: pattern or prefix matching lets attackers redirect codes to controlled hosts; combined with an open redirect it's full account takeover.
- The `state` parameter (or PKCE) binds the callback to the initiating session and blocks login CSRF; `nonce` binds the ID token to the client request and blocks token replay.
- Tokens should be sender-constrained where the stakes justify it: DPoP (RFC 9449) or mTLS-bound tokens turn a stolen bearer token into a useless string.

## Apex practices
- Keep tokens out of browser-persistent storage: for SPAs prefer the backend-for-frontend pattern (tokens in the BFF, session cookie to the browser) or in-memory tokens with refresh-token rotation and reuse detection.
- Scope narrowly and audience-restrict: mint access tokens per resource server (`aud`), request minimal scopes, and use RFC 8707 resource indicators rather than one god-token.
- Use short access-token TTLs (5–15 min) with rotating refresh tokens; a refresh-token replay (old token reused after rotation) should revoke the whole grant chain.
- For microservice hops, exchange tokens (RFC 8693) to preserve the end-user identity down the chain instead of forwarding the original token everywhere.

## Pitfalls
- Building login on `access_token` in a callback query string — tokens in URLs leak via logs, referrers, and browser history.
- Accepting ID tokens without checking `aud` matches your client ID, letting a token minted for a malicious app log into yours.
- Trusting IdP email claims for account linking without `email_verified`, enabling pre-hijack account takeover.

## Tools & references
RFC 6749/6750, RFC 9700 (Security BCP), OAuth 2.1 draft, OIDC Core spec, RFC 7636 (PKCE), RFC 9449 (DPoP), RFC 8693 (token exchange), oauth.net, Keycloak/Auth0/Okta docs.
