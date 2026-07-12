# Layer 2 Rollups

## Scope
Off-chain transaction execution with on-chain settlement: optimistic rollups (retro-active verification), zk-rollups (proofs), and state channels.

## Core principles
- Rollups execute transactions off-chain and batch them on-chain, reducing per-transaction cost by ~100x (amortized across 1000s of txs).
- Optimistic rollups assume correctness by default; anyone can submit a fraud proof to challenge a batch, triggering on-chain verification and rewinding if the batch is invalid.
- Zk-rollups prove correctness cryptographically; every batch includes a ZK proof, so no challenge period is needed and finality is instant.
- State channels (Raiden, Lightning) are two-party rollups: participants sign state updates off-chain and settle on-chain only when disagreement arises.
- The security model depends on liveness (at least one honest participant watching the chain) and the availability of historical state to reconstruct it.

## Apex practices
- Arbitrum (optimistic) and Polygon Hermez (zk) are production rollups; they differ in latency (challenge period vs. instant), throughput, and proving cost.
- Sequencer (the entity ordering transactions) is a centralization risk; if the sequencer censors txs, no L2 transaction happens but users can force include via L1.
- Bridging from L1 to L2 requires trust in the bridge design; canonical bridges (operated by the L2 team) are safer than third-party bridges.
- Composability across rollups is limited; swapping tokens between L2s requires exiting to L1 and re-entering, or trusting a bridge protocol.

## Pitfalls
- Challenge period (usually 7 days in optimistic rollups) means no absolute finality; a delayed fraud proof can reorg your transaction.
- Withdrawal delays: exiting L2 requires proving your balance on L1, which takes time (7+ days + proof generation).
- Cross-rollup liquidity fragmentation; each rollup has its own pool of tokens and users, so prices diverge and swaps are expensive.

## Tools & references
Arbitrum (optimistic rollup), Polygon Hermez (zk-rollup), StarkNet (zk-rollup), Optimism (optimistic rollup), Raiden (state channels), Lightning Network (BTC state channels), rollup scalability trilemma paper.
