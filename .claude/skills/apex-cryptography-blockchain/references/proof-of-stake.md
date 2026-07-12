# Proof of Stake

## Scope
Economic consensus where validators stake capital (not compute) and are slashed for misbehavior; block proposals and finality based on staked weight.

## Core principles
- Validators lock coins as collateral; slashing (destruction) of stake is the penalty for equivocation (voting for conflicting blocks) or non-participation.
- Economic security is based on the cost to attack: an attacker must own > 1/3 of staked capital to corrupt 2f+1 validators (in BFT terms), and slashing makes that ownership costly.
- Staking pools (delegated PoS) allow small holders to participate without running validators; the pool operator is the validator and distributes rewards.
- Randomness for validator selection prevents attackers from predicting who proposes the next block and attacking them; chains use VRFs (Verifiable Random Functions) or threshold schemes.
- Lockup periods (unbonding time) prevent a validator from withdrawing after equivocating, during which the protocol can detect and slash the offense.

## Apex practices
- Validator entry requires a minimum stake (Ethereum 32 ETH) to make 51% attacks expensive; higher minimums reduce network decentralization but increase security.
- Slashing multipliers scale penalties with the number of simultaneous validators offline; this incentivizes coordinated recovery rather than network fragmentation.
- Finality delays (usually 1-2 epochs after attestation) allow the protocol to detect and punish validators before blocks are finalized.
- Delegation markets and MEV (Maximal Extractable Value) rewards create incentives to run validators; but high MEV can lead to censorship (users unable to include txs) or centralization.

## Pitfalls
- Weak randomness for validator selection (seedable from public blockchain state) allows attackers to grind the random number until they're selected, then mount attacks.
- Allowing validators to exit instantly (no unbonding period) means an attacker can fork, slash themselves for cheap, and repeat.
- Over-concentration of stake in one entity; even with slashing, if 50%+ of stake is controlled by one entity, they can permanently censor the network.

## Tools & references
Ethereum 2.0 (Casper FFG + LMD GHOST), Polkadot (BABE + GRANDPA), Solana (PoH + tower BFT), Cosmos (Tendermint PoS), MEV-Boost (Flashbots), Lido (largest Ethereum staking pool), slashing penalties (Ethereum research).
