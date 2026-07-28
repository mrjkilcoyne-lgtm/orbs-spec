# Consensus Algorithms

## Scope
Reaching agreement on state across a distributed network despite Byzantine faults: PBFT, practical Byzantine fault tolerance, leader-based and leader-free consensus.

## Core principles
- Byzantine fault tolerance (BFT) tolerates up to 1/3 corrupted participants; if > 1/3 are corrupted, no protocol can guarantee safety without synchrony assumptions.
- Consensus requires at least two rounds of communication in the asynchronous model (proven impossible to do in one round); practical protocols use timeouts and view changes to handle asynchrony.
- Finality comes in two flavors: probabilistic (as more blocks extend a chain, reorg probability → 0, as in Nakamoto consensus) and absolute (once 2/3+ of validators attest, reorg is cryptographically impossible, as in BFT).
- Liveness is forfeit if the network partitions or validators crash — safety must hold, but new blocks may stop being created; a good protocol prioritizes safety.
- Voting power concentration (Tendermint validator set, Ethereum staking) makes BFT practical (smaller validator count = faster consensus) but centralizes governance; chains optimize for throughput vs. decentralization.

## Apex practices
- PBFT (Practical Byzantine Fault Tolerance) is the template: leader proposes, replicas vote in two phases (prepare, commit), 2f+1 required to reach quorum (tolerate f faults).
- Tendermint (and Cosmos SDK) implements PBFT with instant finality, validator rotation, and Byzantine accountability (slashing for provable misbehavior).
- View changes (leader timeout or accusation) must avoid safety violations; tie view changes to timers and require supermajority agreement on the new leader.
- Validator incentives are critical: in Nakamoto consensus (PoW), miners are paid to extend the heaviest chain; in PoS, validators lose stake (slashing) for equivocation or censorship.

## Pitfalls
- Assuming a network is synchronous when it's asynchronous; protocols without timeouts can deadlock and never reach finality.
- Validator set can change mid-epoch without coordination, allowing an attacker to join undetected and fork the chain.
- Finality gadgets (Casper FFG) added to probabilistic chains require careful integration to ensure the gadget and the chain don't contradict each other.

## Tools & references
PBFT (Castro-Liskov 1999), Tendermint (BFT consensus engine), Hotstuff (leader-based, pipelined BFT), Algorand (asynchronous BA), Casper FFG (Ethereum finality), OWASP blockchain consensus taxonomy.
