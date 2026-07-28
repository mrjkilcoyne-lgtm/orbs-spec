# Authentication

## Scope
Verifying who a principal is: password handling, MFA, passkeys, session management, and account recovery.

## Core principles
- Store passwords only as salted, memory-hard hashes — Argon2id (or scrypt/bcrypt with sane cost) per OWASP Password Storage guidance; a fast hash like SHA-256 falls to GPU cracking at billions of guesses/second.
- Follow NIST SP 800-63B: length over composition rules (allow 64+ chars, drop mandatory rotation and "one uppercase one symbol" theater), check candidates against breached-password corpora.
- MFA strength is ordered: phishing-resistant WebAuthn/passkeys > TOTP > SMS (SIM-swap prone); push-based approvals without number matching fall to MFA-fatigue attacks.
- Sessions are credentials: generate IDs with a CSPRNG, rotate on privilege change (login, elevation) to kill session fixation, set Secure + HttpOnly + SameSite, and enforce absolute plus idle timeouts.
- Account recovery is part of the authentication boundary — a passkey-protected account with email-link recovery is exactly as strong as the email account, so recovery must be rate-limited, logged, and step-up verified.

## Apex practices
- Make authentication uniform-cost and uniform-response: same latency and same error message for unknown-user vs wrong-password to prevent user enumeration; hash even for nonexistent users.
- Rate-limit and add proof-of-work/CAPTCHA per (IP, account) pair, and detect credential stuffing via per-account failure spikes across many IPs — stuffing looks nothing like brute force on one account.
- Offer passkeys as the primary factor with attestation where policy needs it; keep one phishing-resistant factor mandatory for admin and high-risk roles.
- Notify users on new-device login and credential changes, and provide a "sign out everywhere" that actually invalidates server-side session state.

## Pitfalls
- Building a custom password reset with predictable or long-lived tokens — reset tokens must be single-use, short-TTL, hashed at rest, and bound to the account.
- Comparing secrets with non-constant-time equality, leaking validity through timing.
- Trusting "remember me" cookies as full authentication for sensitive actions instead of requiring step-up re-auth.

## Tools & references
NIST SP 800-63B, OWASP Authentication & Password Storage Cheat Sheets, WebAuthn/FIDO2 spec, Argon2 (PHC winner), Have I Been Pwned k-anonymity API.
