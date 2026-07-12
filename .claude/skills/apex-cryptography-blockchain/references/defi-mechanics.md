# DeFi Mechanics

## Scope
Core protocols and interactions in decentralized finance: liquidity pools, AMMs, lending, liquidations, and composability risks.

## Core principles
- Automated market makers (AMMs) use the x*y=k formula (Uniswap v2): swaps adjust prices to maintain the product; anyone can provide liquidity and earn fees.
- Impermanent loss (IL) happens when a pool's price diverges from external prices — a LP's share is worth less than if they'd held the underlying assets.
- Collateralized lending (MakerDAO, Aave) requires overcollateralization to ensure solvency; falling collateral prices trigger liquidations that convert collateral to cash and repay loans.
- Liquidations are auctions where third parties repay part of a loan and seize collateral at a discount; if no liquidator acts, the lender becomes insolvent.
- Flash loans are uncollateralized loans that must be repaid in the same transaction; they enable MEV attacks (borrow, manipulate price, arbitrage, repay), but also legitimate arbitrage.

## Apex practices
- Liquidity concentration (Uniswap v3, Curve's concentrated liquidity) improves capital efficiency but increases IL — LPs must monitor and rebalance positions.
- Use price oracles (Chainlink, Uniswap TWAP) instead of spot prices to defend against flash loan attacks.
- Multi-hop swaps (route through multiple pools) can be cheaper than direct swaps; slippage protection (minimum output) prevents sandwich attacks.
- Liquidation mechanics should be automatic (liquidation contracts trigger when health factor < 1) to prevent cascading insolvencies.

## Pitfalls
- Using spot prices from a single pool for collateral valuation; flash loan attacks manipulate spot price and drain collateral.
- Liquidity providers not accounting for impermanent loss; asymmetric price movements make LPing riskier than hodling.
- Liquidation cascades (Aave's 2020 flash loan attack on sUSD): one liquidation triggers another, causing a collateral spiral.

## Tools & references
Uniswap (v2, v3, v4), Curve (stablecoin AMM), Aave (lending), MakerDAO (DAI stablecoin), Balancer (liquidity pools), Yearn (yield farming), MEV-Inspect (MEV tracking), sandwich attacks (Flashbots MEV-Geth).
