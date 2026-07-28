# Hash Functions

## Scope
Fixed-output digests that are (nearly) collision-resistant, preimage-resistant, and avalanche-effect preserving: SHA-3, BLAKE2, merkle trees.

## Core principles
- Collision resistance, preimage resistance, and second-preimage resistance are independent properties — a hash can be weak in one while strong in others; SHA-1 is broken for collision, but preimage-resistant.
- Merkle trees compose single-element hashes into a tree where every path is verifiable independently; changing one leaf requires recomputing only O(log n) hashes, not all n.
- SHA-3 (Keccak) and BLAKE2 are modern standards; MD5 and SHA-1 are cryptographically broken and must not be used for security (no birthday-day attacks, no collision forgeries).
- Salting a hash (adding random data) prevents rainbow tables and multi-target attacks; without salt, an attacker can precompute hashes for 10M common passwords once and crack all users simultaneously.
- Hash output length matters: 256-bit hashes (SHA-256, BLAKE2b-256) resist brute-force collision attacks and birthday attacks; 128-bit hashes have only 2^64 security margin.

## Apex practices
- Use BLAKE2 or SHA-3 for new systems; SHA-256 is acceptable and widely supported, but slower and less flexible than BLAKE2.
- For password hashing, use a KDF (Argon2, not a bare hash); Argon2 is a hash designed for passwords, not for messages.
- Merkle trees in blockchains include the leaf count to prevent extension attacks where an attacker appends new leaves.
- Use different hash functions for different purposes: one for integrity checks, another for merkle trees, another for cryptographic proofs — context-specific domain separation prevents collisions being weaponized across domains.

## Pitfalls
- Using SHA-1 or MD5 for security; they are broken and known to be attackable.
- Hashing passwords with a plain hash instead of a KDF; 10 billion SHA-256 guesses per second are feasible on a GPU.
- Merkle tree implementations without leaf-count or empty-tree safeguards; an attacker can forge a proof of a non-existent element.

## Tools & references
BLAKE2 (fast, secure, reference implementation), SHA-3 (NIST standard, Keccak family), OWASP password storage guidelines, Merkle tree verification (OpenTimestamps, Certificate Transparency), NIST SP 800-32 (hash-function spec).
