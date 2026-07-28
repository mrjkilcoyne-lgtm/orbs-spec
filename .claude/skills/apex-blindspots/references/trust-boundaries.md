# Trust Boundaries

## Scope
The blindspot of implicit trust: treating input as friendly because of where it seems to come from — users, internal services, files, headers, webhooks, LLM output.

## Core principles
- Trust is a property of the boundary, not the data: the same string is safe or hostile depending on which side of validation it stands; every system diagram should show where untrusted becomes trusted, and each crossing needs a checkpoint.
- "Internal" is a feeling, not a security property: internal services get compromised, employees get phished, VPCs get misconfigured — data from another service deserves validation because that service's compromise shouldn't cascade into yours (the zero-trust argument in miniature).
- Injection is one bug with many costumes: SQL, shell, HTML/XSS, path traversal, header, log, prompt injection — all are "data interpreted as code/instructions in a downstream context"; the universal fix is contextual encoding/parameterization at the point of interpretation, not sanitizing at entry.
- The client is the attacker's IDE: prices, roles, IDs, hidden fields, disabled buttons — anything enforced only client-side is a suggestion; authorization re-checks on the server per request, against the authenticated identity, per resource.
- Deserialization and file parsing are trust decisions: a YAML file, a pickle, an uploaded image, an Excel sheet — parsers execute grammar-shaped input, and rich formats have rich attack surfaces; parse untrusted data with hardened, least-power parsers.

## Detection tests
- Trace each input to its origin: at what exact line does this data earn trust, and what check happens there?
- What does this code do with input from a compromised (not just buggy) upstream?
- Is any authorization decision made from data the client can edit (IDs, roles, prices in the payload)?

## Countermeasures
- Validate at every boundary with allowlists on structure (schema validation) and encode at every sink for its context (parameterized SQL, HTML escaping, shell arg arrays).
- Make trust levels visible in code: types like UntrustedString/SanitizedHtml, or naming conventions, so the boundary crossing is greppable.
- Fuzz the parsers and replay hostile payloads (OWASP cheat sheets, naughty strings) as regression tests — the boundary is only as real as its test suite.

## Tools & references
OWASP cheat sheet series, threat-model boundary diagrams (STRIDE), parameterized query APIs, zero-trust architecture papers.
