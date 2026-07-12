# Symmetric Cryptography

## Scope
Encryption and authentication using a single shared secret: AES, stream ciphers, block modes, and authenticated encryption.

## Core principles
- AES is the standard (NIST approved, hardware-accelerated, 256-bit variant for long-term secrets) — use it until quantum breaks it; avoid homebrew or "stronger" cipher misunderstandings.
- Block modes matter as much as the cipher: ECB (never), CBC (needs PKCS7 padding and IV), CTR (nonce-based, parallelizable), GCM (authenticated, NIST approved for AEAD).
- Authenticated encryption (AEAD) is mandatory for most uses: GCM, ChaCha20-Poly1305, or AES-GCM prevent padding oracle and unauthenticated ciphertext attacks.
- Nonce/IV reuse is catastrophic: CTR and GCM with reused nonces leak plaintext; generate cryptographically random nonces, never encode sequence numbers as IVs.
- Key derivation from passwords uses KDF (PBKDF2, Argon2) to slow down brute force; raw password hashing has no defense against modern GPUs.

## Apex practices
- Use libraries, not implementations: libsodium (NaCl), BoringSSL, or language standard libraries — cryptographic implementation is a minefield for integer overflow, side channels, and timing attacks.
- For passwords: Argon2id (memory-hard, GPU-resistant, time-hard), minimum 2^16 memory, minimum 3 iterations, salt from CSPRNG.
- Authenticate everything encrypted: AES-GCM or ChaCha20-Poly1305 as the default, never unauthenticated CTR or CBC.
- Rotate keys on a schedule (annual for long-term secrets, per-session for ephemeral); design systems for transparent key rotation without decrypting all historical data.

## Pitfalls
- Encrypting with AES-CBC and no authentication, then padding-oracle attacks decrypt ciphertext even without the key.
- Deriving multiple keys from one master without key derivation: XORing or concatenating the master key yields keys that can be combined to recover it.
- Hardcoding IVs or using predictable nonces; every message with a reused nonce in CTR mode is compromise.

## Tools & references
libsodium/NaCl (reference implementations), OWASP Cryptographic Failure guide, NIST SP 800-38D (GCM spec), OWASP "A02 Cryptographic Failures" (OWASP Top 10), Argon2 (PHC winner).
