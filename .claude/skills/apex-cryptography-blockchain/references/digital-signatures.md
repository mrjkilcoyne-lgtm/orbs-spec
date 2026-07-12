# Digital Signatures

## Scope
Proving authorship and non-repudiation: ECDSA, BLS, Schnorr, signature verification, and threshold signatures.

## Core principles
- A signature is a proof that the signer knows the private key and authorized the message — not confidentiality, but authenticity and non-repudiation.
- ECDSA (RFC 6090) requires a cryptographically random nonce per signature; reusing or weakly generating the nonce leaks the private key (Sony's PlayStation hack, Java SecureRandom failures).
- Schnorr signatures are simpler than ECDSA (easier to prove secure), support threshold signatures, and are becoming standard (BIP 340 in Bitcoin Taproot, Ethereum's signature aggregation plans).
- BLS signatures enable signature aggregation: multiple signatures on the same message combine into one; used in consensus (proof-of-stake finality, validator aggregation) to reduce on-chain data.
- Batch verification (verifying multiple signatures in one check) is faster than verifying individually; protocols use this for scalability.

## Apex practices
- Always hash the message before signing (H(m) where H is SHA-256 or better), and specify the hash function in the protocol to prevent hash-swapping attacks.
- Use Ed25519 (deterministic ECDSA on Edwards curves) over ECDSA(SHA-256) — it's simpler, faster, and removes the nonce-generation risk.
- In multi-signature schemes, require a threshold (t of n) and ensure the threshold is enforced before signing; Shamir secret sharing allows t parties to sign without any party seeing the full key.
- Test signature verification against malformed inputs (invalid curve points, wrong hash length, zero values) to catch parsing bugs.

## Pitfalls
- Signing user-supplied messages without hashing, or hashing with a different function than the verification code expects.
- Nonce reuse in ECDSA, which immediately leaks the private key; even weak nonce generation (seeded with time, not CSPRNG) can be exploited.
- Trusting a signature without verifying it was created by the expected party — the public key must be authenticated (pinned, in a certificate, or on-chain).

## Tools & references
Ed25519 (IETF RFC 8032, reference implementation), ECDSA (RFC 6090), BLS (RFC 9115 draft, Boneh-Lynn-Shacham), Schnorr (BIP 340), threshold schemes (Shamir secret sharing), batch verification (Karalias, Kiayias).
