# Key Management

## Scope
Generating, storing, rotating, and protecting cryptographic keys throughout their lifecycle.

## Core principles
- A key is only as strong as its generation entropy — keys from weak RNGs (time-seeded, /dev/urandom, or JavaScript Math.random) are guessable.
- Key derivation functions (KDFs) generate multiple independent keys from a single master key using context (algorithm, key type, index) to prevent attacks where a subkey leaks the master.
- Private keys must never touch plaintext storage; they live in a key management service (KMS), hardware security module (HSM), or encrypted key bundle with the encryption key separated.
- Key rotation (replacing old keys with new ones) is mandatory for long-lived systems — old keys can be compromised without the operator knowing, so losing access to them after rotation is acceptable.
- Key escrow (a third party holding a copy of the key) defeats the purpose of asymmetric cryptography; threshold schemes allow recovery without a single escrow holder.

## Apex practices
- Use HKDF (HMAC-based KDF) to derive session keys from a shared secret; include domain-specific context (algorithm OID, party identifier, purpose) in the info parameter.
- For application keys, store private keys in a KMS (AWS KMS, Azure Key Vault, HashiCorp Vault) and rotate them automatically; application code never sees the plaintext key.
- For hardware security modules (HSMs), use FIPS 140-2 Level 3 devices for sensitive keys; they enforce tamper-detection and non-extractable key storage.
- Implement key versioning: tag each encrypted message or token with a key ID so you can rotate without decrypting all historical data at once.

## Pitfalls
- Storing the private key in the same location as the ciphertext or in code; compromise of either reveals the other.
- Rotating keys but forgetting to update the key ID in the metadata, leading to decryption failures.
- Deriving multiple keys from one master without a KDF, or using a KDF without domain-separation — multiple keys can be combined to recover the master.

## Tools & references
HKDF (RFC 5869), NIST SP 800-132 (PBKDF2 spec), OWASP secrets management, HashiCorp Vault, AWS KMS/CloudHSM, Thales Luna HSM, key rotation best practices (Google Cloud), envelope encryption pattern.
