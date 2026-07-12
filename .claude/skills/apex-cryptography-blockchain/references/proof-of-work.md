# Proof of Work

## Scope
Economic consensus where miners invest compute (hardware, electricity) to solve cryptographic puzzles; mining difficulty adjusts to maintain block time.

## Core principles
- Proof of work (PoW) is a computational puzzle: hash(block) must be <= target (e.g., leading zeros in SHA-256); finding it requires 2^d expected hashes where d is difficulty.
- Difficulty adjusts every N blocks (Bitcoin: 2 weeks, Ethereum pre-merge: hourly) to keep block time constant; if hashrate increases, difficulty rises, and vice versa.
- 51% attack requires controlling > 50% of hashrate for a sustained period; with > 50% power, an attacker can reorg the chain, double-spend, and censor transactions.
- Nakamoto consensus relies on the chain with the most work being the canonical version (longest chain rule); this is probabilistically secure but never has absolute finality.
- ASIC mining (application-specific integrated circuits) is economically dominant for SHA-256; CPU/GPU-friendly PoW algorithms (Monero's RandomX) try to resist ASIC dominance.

## Apex practices
- Mining pools (distribute work among miners, combine rewards) concentrate hashrate; solo mining is economically unviable for most participants.
- Selfish mining attacks (withholding blocks to gain advantage) are theoretically possible but require > 33% hashrate and break down with network synchrony assumptions.
- Block difficulty is the primary lever for security; lower difficulty = easier attack, higher difficulty = higher variance in block time.
- Merge/switch times allow switching between PoW chains; Monero does this (~every 3.5 years) to resist ASIC centralization.

## Pitfalls
- Assuming blocks are final just because they're deep in the chain; after a 51% attack, reorg can be arbitrarily deep (no probabilistic guarantee).
- Centralization in mining pools means a few operators can censor or fork the chain; even if no single entity controls 51%, coordination of 2-3 largest pools can.
- Hard forks with PoW algorithm changes can lead to contentious community splits (Bitcoin Gold, Ethereum Classic) if the change is not universal.

## Tools & references
Bitcoin (SHA-256, 10-min blocks), Ethereum pre-merge (Ethash), Monero (RandomX CPU-friendly), Litecoin (Scrypt ASIC-resistant), mining pool protocols (Stratum), difficulty adjustment algorithms (Bitcoin's retarget).
