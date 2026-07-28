# Fintech Systems

## Scope
Financial platforms: payments, lending, trading, compliance (AML/KYC), settlement, and systems that move or manage money with regulatory oversight.

## Core principles
- Money is accurate to the cent (or satoshi, in crypto): all calculations are fixed-point, never floating-point; rounding rules are explicit and auditable (round-half-up is different from banker's rounding).
- Transactions are irreversible once settled; reversals are separate transactions; immutability is a feature, not a bug (essential for compliance and audit trails).
- Regulations are numerous and territorial: US (SEC, FINRA), UK (FCA), EU (MiFID II), Asia (different per country); compliance is non-negotiable and changes frequently (requires legal review of code).
- Settlement is the critical path: trades execute, then settle (funds/securities move) T+0 (crypto) to T+2 (stock) — latency in settlement costs money; efficiency is existential.
- Fraud detection is asymmetric: legitimate customers must not be blocked (false positives destroy trust), but fraud must be caught (false negatives are direct loss); models and rules balance this.

## Apex practices
- Use ledger-based accounting (double-entry: every transaction is a debit and credit pair) so balance always equals zero — bugs are detectable.
- Implement idempotency on all payment operations: retries must produce the same result (same transaction ID, no double-charge).
- Separate settlement from authorization: a card can be authorized but not yet settled, requiring manual reconciliation and dispute handling.
- Log all decisions (compliance approvals, risk decisions, trade execution) with timestamp and actor; audit trails are legal requirements.

## Pitfalls
- Using floating-point for money calculations; it introduces rounding errors that compound.
- Designing transaction systems without idempotency; retries after network failures cause double-charges.
- Underestimating regulatory complexity; building without legal review ensures rework.

## Tools & references
ISO 20022 (payment messaging standard), PCI DSS (payment security), FinCEN guidance (AML), Stripe/Square APIs (payment processors), FIX protocol (trading), double-entry accounting principles.
