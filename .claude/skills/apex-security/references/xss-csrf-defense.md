# XSS / CSRF Defense

## Scope
Defending browser-facing applications against cross-site scripting (script execution in the victim's origin) and cross-site request forgery (riding the victim's ambient credentials).

## Core principles
- XSS defense is contextual output encoding: the same string needs different encoding for HTML body, attribute, JavaScript string, URL, and CSS contexts — modern framework templating (React JSX, Vue, Angular) does this by default, and XSS today mostly enters through the escape hatches (`dangerouslySetInnerHTML`, `v-html`, `bypassSecurityTrust*`).
- DOM XSS never touches the server: source (location.hash, postMessage, storage) flows to sink (`innerHTML`, `eval`, `document.write`) entirely client-side — server-side filtering can't see it; Trusted Types (CSP directive) makes these sinks require typed, policy-vetted values.
- Content-Security-Policy is the XSS backstop, not the fix: a strict nonce/hash-based policy (`script-src 'nonce-…' 'strict-dynamic'`) blocks injected inline scripts even after an encoding failure; allowlist-based CSPs are widely bypassable (JSONP endpoints, Angular gadgets — see Google's "CSP Is Dead" research).
- CSRF exists because browsers attach cookies to cross-site requests automatically; the defenses are `SameSite=Lax/Strict` cookies (now default-Lax in Chromium) plus a synchronizer or signed double-submit token for anything SameSite can't cover (subdomain trust, older clients).
- Bearer-token auth in headers is inherently CSRF-immune (the attacker can't set the header cross-origin) but trades into XSS-token-theft risk — the storage-vs-cookie decision is a trade between the two attack classes.

## Apex practices
- Deploy CSP in `Content-Security-Policy-Report-Only` first, watch the violation reports, then enforce; add `frame-ancestors` (clickjacking), `object-src 'none'`, and `base-uri 'none'` while you're there.
- Sanitize any genuinely-needed rich HTML with DOMPurify server- and client-side; never write your own HTML sanitizer, and re-sanitize after every transformation.
- Verify CSRF protection is on for every state-changing route including "invisible" ones (logout, email change, API-key creation) and confirm GET handlers never mutate state.
- Set the full defensive header suite: `SameSite` on all cookies, `X-Content-Type-Options: nosniff`, HSTS, and use `Origin`/`Sec-Fetch-Site` header checks as a cheap additional CSRF layer.

## Pitfalls
- Escaping for HTML body context but injecting into an event handler or `javascript:` URL — attribute and URL contexts have their own parsers and their own bypasses.
- Believing SameSite alone finishes CSRF: it doesn't cover same-site subdomain attackers, `Lax` still sends cookies on top-level GET navigations, and cross-scheme (http→https) edge cases have bitten real apps.
- Reflecting user input into JSON served as `text/html`, or into inline `<script>` blocks without `<` escaping — script-context injection slides past HTML encoding.

## Tools & references
OWASP XSS Prevention & CSRF Prevention Cheat Sheets, CSP Level 3 spec, Trusted Types, DOMPurify, Google CSP Evaluator, PortSwigger Web Security Academy XSS/CSRF labs.
