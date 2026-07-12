# Cross-Chain Bridges

## Scope
Protocols for asset and data transfer between blockchains: atomic swaps, wrapped tokens, federated bridges, and security models.

## Core principles
- A bridge is a security boundary; it's only as safe as its weakest component (consensus, validator set, oracle).
- Wrapped tokens represent a 1:1 claim on the original token held by the bridge; if the bridge is compromised, wrapped tokens can be minted unbacked.
- Atomic swaps (HTLC, adaptor signatures) enable trustless cross-chain swaps without a bridge operator, but require both chains to support the necessary cryptography.
- Light clients (running on-chain verification of the other chain's consensus) are the gold standard for security; they require the other chain to be lightweight (low validator count, small headers).
- Validator committees and thresholds (m-of-n signatures) are weaker than full consensus verification but faster and cheaper on-chain.

## Apex practices
- Use light clients (IBC for Cosmos chains, Polkadot XCM for parachains) for highest security; bridges verified by light clients inherit the security of the chain they verify.
- Wrapped tokens should have well-defined custody (who holds the reserve?) and redemption mechanics (how do users unwrap?); unknown operators raise red flags.
- Liquidity networks (Stargate, Axelar) use incentives and algorithmic routing to overcome fragmented bridge liquidity; they tolerate bridge delays and liveness failures.
- Monitor TVL (total value locked) in bridges; newer bridges with < $10M TVL carry high risk (worth exploiting), while multi-billion-dollar bridges have more scrutiny.

## Pitfalls
- Bridge hacks are common (Ronin $625M, Poly Network $625M, Wormhole $325M); many are due to weak validator sets or private key compromise.
- Wrapped token depegs if the bridge fails; users holding wstETH on L2 during an L2 fork lose the bridge (no longer 1:1 with Ethereum ETH).
- Liquidity fragmentation: each bridge has its own pool of wrapped assets, leading to slippage; swapping through a bridge is expensive and slow.

## Tools & references
Uniswap V3 for cross-chain (via bridge), Stargate (cross-chain DEX), Axelar (GMP — general message passing), Wormhole (multi-chain portal), IBC (Inter-Blockchain Communication), atomic swaps (HTLC, adaptor signatures), bridge audits (Trail of Bits, OpenZeppelin).
