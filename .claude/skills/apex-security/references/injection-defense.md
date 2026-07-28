# Injection Defense

## Scope
Preventing untrusted data from being executed as code in any downstream interpreter: SQL, OS commands, LDAP, templates, XML, and deserialization.

## Core principles
- All injection is one bug: data crossing into a code channel. The universal fix is structural separation — parameterized APIs where data can never be parsed as syntax — not escaping, and never blocklist "sanitization."
- Parameterized queries/prepared statements defeat SQLi completely for values, but identifiers (table/column names, ORDER BY) cannot be parameterized — those need strict allowlist mapping from user input to known-safe names.
- Command injection defense is "don't invoke a shell": use exec-style APIs with argument arrays (`execve`, `subprocess.run([...])` without `shell=True`); once a shell parses the string, quoting is an arms race you lose to `$()`, backticks, and IFS tricks.
- Server-side template injection is RCE by design: user input in the template source (not template variables) of Jinja2/Freemarker/ERB hands the attacker the engine's object graph and from there the process.
- Deserializing untrusted data with native serializers (Java `ObjectInputStream`, Python pickle, PHP `unserialize`, YAML full loaders) is arbitrary code execution via gadget chains — use data-only formats (JSON, protobuf) with schema validation.

## Apex practices
- Make the safe path the only path: ORM/query-builder everywhere, a lint/CI rule (Semgrep) that flags string-concatenated SQL and `shell=True`, and code review treats exceptions as security decisions.
- Validate inputs positively at the boundary (type, length, range, allowlisted pattern) as defense-in-depth — validation reduces attack surface but is never the primary control.
- Disable XML external entity resolution (XXE) in every parser explicitly; JAXP, libxml2, and .NET parsers have historically shipped with DTD/entity processing on.
- Run the app with least-privilege downstream credentials: the web app's DB user has no DDL, no cross-schema access, so a residual SQLi reads one schema instead of exfiltrating everything.

## Pitfalls
- Escaping user input "for safety" and then interpolating it anyway — escaping is context-specific and fragile; one missed context (LIKE clauses, JSON-in-SQL) reopens the hole.
- Second-order injection: data stored safely, then read back and concatenated into a query later where it's now "trusted."
- Blind spots beyond SQL: NoSQL operator injection (`{"$gt": ""}` in MongoDB filters), LDAP filter injection, header/log injection (CRLF), and expression-language injection (SpEL, OGNL).

## Tools & references
OWASP Injection Prevention & SQLi Cheat Sheets, CWE-89/77/78/502, Semgrep/CodeQL injection rulesets, sqlmap (authorized testing), Bobby Tables (bobby-tables.com).
