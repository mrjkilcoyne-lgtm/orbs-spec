# OWASP Top 10

## Scope
The canonical taxonomy of web application security risks and how to build defenses against each category.

## Core principles
- Broken Access Control is #1 (A01:2021) for a reason: authorization bugs (IDOR, missing function-level checks, path traversal) are logic flaws no scanner reliably finds — every object access must check ownership server-side.
- Injection (A03) and XSS share one root cause: mixing untrusted data into an interpreter's code channel; the fix is always structural (parameterization, contextual encoding), never sanitization by blocklist.
- Cryptographic Failures (A02) is usually not broken math but broken usage: plaintext PII at rest, TLS terminated then plaintext internally, homegrown crypto, hardcoded keys.
- Insecure Design (A04) says you cannot test your way out of a missing control — a design with no rate limiting or no tenant isolation is insecure regardless of implementation quality.
- The Top 10 is an awareness floor, not a compliance ceiling: use OWASP ASVS for actual requirements coverage and the Top 10 as a shared vocabulary with stakeholders.

## Apex practices
- Map each Top 10 category to a concrete control in your stack and a test that proves it: A01→centralized authorization middleware + IDOR test suite, A03→ORM/parameterized queries + SQLi CI checks, A05→IaC scanning with tfsec/Checkov.
- Treat Vulnerable and Outdated Components (A06) as an SLA problem: automated dependency updates (Dependabot/Renovate) with a patch-latency target (e.g., critical CVEs patched < 7 days).
- Wire Security Logging and Monitoring (A09) to detection: failed authz attempts, auth anomalies, and server-side request patterns must produce alerts someone owns.
- For SSRF (A10), default-deny egress from application hosts and validate URLs against an allowlist resolved at request time — blocklisting 169.254.169.254 is a losing game (DNS rebinding, redirects, IPv6 forms).

## Pitfalls
- Treating a clean DAST scan as "we're OWASP compliant" — access control and design flaws are invisible to scanners.
- Fixing individual findings without the systemic control (patching one IDOR endpoint while forty others use the same pattern).
- Ignoring A08 (Software and Data Integrity Failures): unsigned auto-updates and insecure deserialization are RCE-grade, not hygiene items.

## Tools & references
OWASP Top 10 (2021), OWASP ASVS, OWASP Cheat Sheet Series, OWASP Testing Guide (WSTG), ZAP, Burp Suite.
