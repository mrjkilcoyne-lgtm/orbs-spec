# JWT

## Scope
JSON Web Tokens as signed claim containers: structure, validation discipline, algorithm choices, and revocation strategy.

## Core principles
- A JWT is only as trustworthy as its validation: verify signature, `alg` against an allowlist, `iss`, `aud`, `exp`/`nbf` (with small clock skew), and reject anything else — the historic `alg=none` and RS256→HS256 confusion attacks are both validation failures, not crypto failures.
- Signed ≠ secret: JWT payloads are base64url-encoded plaintext readable by anyone; PII or secrets in claims require JWE or don't belong there.
- Statelessness is the feature and the bug: no server round-trip to validate, but also no server-side revocation — a stolen token is valid until `exp`, so TTL is your blast-radius dial (minutes, not days).
- Pin one asymmetric algorithm per trust relationship (EdDSA or ES256 preferred, RS256 acceptable) and fetch keys by `kid` from a JWKS endpoint with cache + rotation; HS256 shared secrets couple every verifier into a single compromise domain.
- Key rotation must be zero-downtime by design: publish new key in JWKS, start signing with it, keep the old key for verification until the last old token expires.

## Apex practices
- Use a maintained library and its strict mode; hand-rolled parsing is where `alg` confusion and signature-stripping bugs live. Check your library against the known-vulnerabilities list on jwt.io.
- Keep access tokens short-lived (≤15 min) and pair with rotating refresh tokens; for logout/compromise, maintain a denylist of `jti` values with TTL = token lifetime — small because tokens are short.
- Use typed tokens (`typ: at+jwt` per RFC 9068) and distinct `aud` per API so an ID token can't be replayed as an access token and tokens can't cross service boundaries.
- Validate at the edge (gateway) and re-validate at each service — internal networks are not trust boundaries; pass claims onward via a re-signed internal token if you must transform them.

## Pitfalls
- Accepting the `alg` header as instructions rather than checking it against expectations — the verifier chooses the algorithm, never the token.
- Sessions-in-JWT: cramming mutable state (roles, permissions) into long-lived tokens, then discovering revoked admins stay admin until expiry.
- Trusting `kid`/`jku`/`x5u` header values to fetch keys from arbitrary URLs or file paths (key-injection and path-traversal vector); resolve keys only from your configured JWKS.

## Tools & references
RFC 7519 (JWT), RFC 7515/7517 (JWS/JWK), RFC 8725 (JWT Best Current Practices), RFC 9068 (JWT access-token profile), jwt.io library table, PASETO as the opinionated alternative.
