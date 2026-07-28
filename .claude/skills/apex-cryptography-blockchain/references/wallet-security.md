# Wallet Security

## Scope
Cryptocurrency key management, custody, and user-level security: seed phrases, hardware wallets, multisig, and attack vectors.

## Core principles
- A wallet is a key pair (private key, public key); the private key signs transactions and must be kept secret, while the public key (address) is public.
- Seed phrases (BIP-39 mnemonics) are human-readable backups for keys; a 12 or 24-word phrase can regenerate all keys in a hierarchical deterministic (HD) wallet.
- Hardware wallets (Ledger, Trezor) keep the private key offline and require physical confirmation for transactions; they're the gold standard for self-custody.
- Multisig (m-of-n signatures) requires m of n signers to approve a transaction; 2-of-3 is common (user + security company + backup) and resilient to one key being compromised.
- Private key derivation (BIP-32 HD wallets) allows one seed to generate many independent keys without storing separate seeds; each key is isolated.

## Apex practices
- Store seed phrases in a secure location (safe deposit box, metal backup, not cloud storage or plaintext files).
- Use hardware wallets for > $10k in holdings; the convenience cost is worth the security gain.
- Implement multisig for institutional wallets (exchanges, treasuries) — no single person or device can steal funds.
- Test recovery: every year, verify that the seed phrase can regenerate the wallet; delays between backup and recovery reveal problems.

## Pitfalls
- Phishing sites mimicking wallet interfaces (metamask.com clone) harvest seed phrases; users must verify domain names carefully.
- Weak random number generation when creating keys; if the RNG is predictable, the key is guessable.
- Sharing seed phrases or private keys with anyone (recovery services, validators) — anyone with a private key can spend the funds.

## Tools & references
BIP-32 (hierarchical deterministic wallets), BIP-39 (mnemonic code), BIP-44 (derivation paths), Ledger (hardware wallet), Trezor (hardware wallet), MetaMask (software wallet), Gnosis Safe (multisig), OWASP wallet best practices.
