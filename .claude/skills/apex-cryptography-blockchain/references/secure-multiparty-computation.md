# Secure Multiparty Computation

## Scope
Computing a function over secret inputs from multiple parties without any party learning the others' inputs: MPC, threshold schemes, and secret sharing.

## Core principles
- Secret sharing (Shamir, additive, XOR-based) splits a secret into n shares such that any t shares reconstruct it, but fewer than t shares reveal nothing.
- An MPC protocol computes f(x1, x2, ..., xn) where party i knows xi but not xj (j≠i), and no collusion of fewer than t parties learns anything beyond the output.
- Linear secret sharing enables efficient computation of linear functions (addition, subtraction, scalar multiplication) without interaction; nonlinear operations (multiplication) require communication rounds.
- Honest-majority protocols tolerate up to (n-1)/2 corruptions; dishonest-majority protocols (using homomorphic encryption or garbled circuits) tolerate up to (n-1) corruptions but are slower.
- Threshold cryptography applies MPC to signatures: t of n parties can sign without any party knowing the full key, and a coalition of up to (t-1) parties cannot forge signatures.

## Apex practices
- For threshold schemes, use polynomial interpolation (Shamir over finite fields) with secret-independent reconstruction (no party learns the polynomial, only their share).
- Use additive secret sharing for distributed randomness beacons (no single party chooses the random output) — used in Ethereum's RANDAO and DKG protocols.
- Garbled circuits (Yao's protocol) allow two-party MPC with constant interaction rounds; for n > 2 parties, use replicated or threshold MPC for better efficiency.
- Verify commitments (Pedersen commitments, homomorphic encryption) to ensure parties follow the protocol before reconstruction — a corrupted party can manipulate their share.

## Pitfalls
- Assuming a shared honest majority when the network is adversarial; in open networks (no trusted dealer), use dealer-free DKG (Distributed Key Generation).
- Reconstruction without commitment verification; a corrupted party contributes a garbage share and contaminates the output.
- Leaking metadata (response times, message sizes) that correlates with input values; constant-time and constant-size implementations are hard.

## Tools & references
Shamir secret sharing (Shamir, 1979), Pedersen commitments, Yao's garbled circuits, SPDZ (ABY, MP-SPDZ for framework implementations), DKG (FROST, Gennaro-Jarecki), OWASP threshold cryptography, Zcash's MPC ceremony methodology.
