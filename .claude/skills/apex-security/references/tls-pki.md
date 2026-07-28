# TLS / PKI

## Scope
Transport security in practice: TLS configuration, certificate lifecycle, trust chains, and internal PKI.

## Core principles
- TLS 1.3 removed the footguns by construction — no RSA key exchange, no CBC/RC4/EXPORT suites, mandatory forward secrecy (ephemeral ECDHE), 1-RTT handshake; the modern baseline is TLS 1.3 preferred, 1.2 with AEAD suites as floor, everything older off.
- Certificate validation is the whole game for clients: verify the chain to a trusted root, hostname (SAN, not CN), and expiry/revocation — `verify=False` in one HTTP client silently converts TLS into an active-MITM-friendly obfuscation layer.
- Forward secrecy means a recorded ciphertext stream stays safe even if the server's long-term key later leaks — this is why static-RSA key exchange died and why session-ticket keys (which can undo FS) must be rotated aggressively.
- Trust is hierarchical and revocation is weak: CRLs and OCSP fail open in most clients, so short-lived certificates (90 days trending to 47 by 2029 per CA/Browser Forum) plus automation are the practical revocation story.
- Internal traffic needs TLS too: mTLS gives each workload a cryptographic identity (SPIFFE-style SVIDs), replacing IP allowlists that dissolve in dynamic infrastructure.

## Apex practices
- Automate issuance and renewal end-to-end with ACME (Let's Encrypt, or ACME against your internal CA via step-ca/Vault PKI); alert on certs expiring within 2× your renewal interval — expiry outages are the most preventable outage class.
- Run your config through SSL Labs/testssl.sh and pin to the Mozilla "intermediate" profile unless you have measured legacy-client needs; enable HSTS with preload once you're sure.
- Monitor Certificate Transparency logs for your domains — CT is how you discover misissued or rogue certificates for your names.
- For internal PKI, keep the root offline, issue from short-lived intermediates, constrain them (name constraints, EKU), and make workload certs hours-to-days lived so revocation is just non-renewal.

## Pitfalls
- Terminating TLS at the load balancer and running plaintext to the backend on the theory the network is trusted — that theory is what zero trust exists to bury.
- Certificate pinning in mobile apps without a rotation plan, bricking connectivity when the cert rolls.
- Wildcard certs shared across many services: one compromised host impersonates every subdomain.

## Tools & references
RFC 8446 (TLS 1.3), Mozilla SSL Configuration Generator, SSL Labs, testssl.sh, ACME (RFC 8555), Let's Encrypt, step-ca, HashiCorp Vault PKI, SPIFFE/SPIRE, crt.sh for CT search.
