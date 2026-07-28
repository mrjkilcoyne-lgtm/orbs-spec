# Asymmetric Cryptography

## Scope
Public-key cryptography for encryption, key exchange, and authentication without shared secrets: RSA, ECDSA, elliptic curves.

## Core principles
- Elliptic-curve cryptography (P-256, secp256k1, Curve25519) is preferred over RSA: smaller keys, faster operations, fewer padding pitfalls, and equivalent security.
- Key exchange establishes a shared secret over public channels (Diffie-Hellman, ECDH); the resulting secret is then used for symmetric encryption — asymmetric encryption of bulk data is too slow.
- RSA requires careful padding: PKCS#1 v1.5 padding is vulnerable to Bleichenbacher attacks; use OAEP for encryption and PSS for signatures.
- Elliptic curves are defined by their parameters (prime field, cofactor, generator order) — validating input points is essential to prevent small-order attacks or invalid-curve injection.
- Forward secrecy requires ephemeral keys: even if a long-term private key is compromised, past session keys cannot be recovered because they were derived from now-deleted ephemeral keys.

## Apex practices
- Use Curve25519 (Montgomery form) for key exchange and Ed25519 (Edwards form) for signatures; these curves resist timing attacks and have small, tight parameter choices.
- In TLS 1.3, ECDH(secp256k1) or X25519 with ephemeral keys is mandatory, and DHE (static Diffie-Hellman) has been removed for good reason.
- Generate keys with a CSPRNG (never a weak RNG); if an RNG is weak, the private key is not random and the cryptosystem fails completely.
- Validate public keys received from untrusted parties: check they are in the correct subgroup and reject points at infinity or of low order.

## Pitfalls
- Using RSA without OAEP padding; PKCS#1 v1.5 is broken to Bleichenbacher attacks even if you think you're checking padding properly.
- Reusing ephemeral keys (thinking they're long-term) — that defeats forward secrecy and opens you to key-recovery attacks.
- Signing user-supplied data without hashing first; if two payloads collide in the hash, both are validly signed.

## Tools & references
Curve25519 and Ed25519 (IETF RFC 7748, RFC 8032), ECDH (RFC 5480), TLS 1.3 (RFC 8446), OWASP "Cryptographic Failures" guide, libsodium for reference implementations.
