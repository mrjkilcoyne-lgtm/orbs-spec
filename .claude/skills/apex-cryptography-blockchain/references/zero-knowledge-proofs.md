# Zero-Knowledge Proofs

## Scope
Proving a statement is true without revealing any information except that the statement is true: zk-SNARKs, zk-STARKs, and applications in privacy and scalability.

## Core principles
- A zk proof has three properties: completeness (true statements are provable), soundness (false statements are unprovable with high probability), and zero-knowledge (the proof reveals nothing but truth of the statement).
- zk-SNARKs (Succinct, Non-interactive Arguments of Knowledge) produce constant-size proofs with linear-time verification; they require a trusted setup (setup ceremony) that if compromised ruins soundness.
- zk-STARKs (Scalable, Transparent ARguments of Knowledge) don't require a trusted setup and resist quantum attacks, but proofs are larger and verification slower than SNARKs.
- Constraint systems (R1CS, AIR, PLONKish) encode the problem as polynomial equations; proving knowledge of a solution is equivalent to proving the system is satisfiable.
- Lookup arguments (Plookup, LogUp) allow efficient proof of membership in a table without verifying the table contents; used in blockchains for range checks and global state access.

## Apex practices
- Use zk-SNARKs for privacy (hiding transaction amounts, sender/receiver) and scalability (rollups compressing many proofs into one).
- Verify the constraint system and setup ceremony — many ZK protocols have been broken by subtle bugs in the system or assumptions about the ceremony.
- Use established libraries (circom for circuit design, rapidsnark or halo2 for proving) rather than rolling your own — the math is unforgiving.
- For privacy applications, understand the anonymity set (larger is better for hiding among many) and ensure the proof scheme doesn't leak metadata through size or timing.

## Pitfalls
- Assuming privacy from a zk proof alone; transaction graph analysis, metadata, and side channels often leak more information than the proof hides.
- Weak constraint systems that don't fully capture the problem (e.g., a range check that doesn't actually enforce bounds).
- Reusing randomness (the "witness" in the proof) across multiple proofs, which allows an attacker to extract it.

## Tools & references
Circom (circuit language), rarith (proof system), halo2 (PLONK variant), Aztec, StarkWare Cairo, Zcash Halo (trusted-setup-free SNARKs), OWASP ZK article, Vitalik's ZK explainer series.
