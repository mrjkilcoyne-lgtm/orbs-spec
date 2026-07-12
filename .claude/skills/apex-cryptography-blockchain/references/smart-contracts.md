# Smart Contracts

## Scope
Deployable code on blockchains that execute autonomously and are immutable once deployed; audit patterns, upgrades, and formal verification.

## Core principles
- Smart contracts are immutable once deployed; bugs can be exploited without patches — security in the contract and on-chain verification matter more than traditional software.
- State changes are transactions (recorded on-chain, verified by all nodes, finalized in consensus) — no "transactions" in the ACID sense, only state changes replicated across the network.
- Gas metering limits computation: Ethereum charges by opcode execution to prevent infinite loops and DoS; a runaway contract becomes expensive, not a security breach.
- Reentrancy (a callee calling back into the caller during execution) is the classic bug: a contract sends funds before updating balance, the recipient's fallback re-enters and withdraws again.
- Formal verification (mathematical proof that a contract meets a spec) is feasible for small critical contracts; model checkers (TLA+, Z3) and theorem provers (Coq, Isabelle) are tools but require expertise.

## Apex practices
- Use battle-tested libraries (OpenZeppelin, for token contracts, access control) rather than writing primitives.
- Deploy to testnet and audited networks (Ethereum testnets, Polygon testnet) before mainnet; run static analysis (Mythril, Slither) and dynamic testing (Hardhat, Foundry).
- Implement checks-effects-interactions pattern: verify preconditions, update state, then call external contracts; this prevents reentrancy.
- Upgradeable contracts use proxy patterns (delegation, UUPS) — the implementation can change but storage layout must be preserved; OZ's Upgrades plugin enforces this.

## Pitfalls
- Reentrancy bugs (The DAO hack, 2016: $50M stolen); check-effect-interact and ReentrancyGuard mitigate.
- Integer overflow/underflow (fixed in Solidity 0.8+, now reverts instead of wrapping).
- Delegatecall to untrusted code (storage slot conflicts, execution in the calling contract's context can be hijacked).

## Tools & references
OpenZeppelin Contracts, Hardhat (testing framework), Foundry (Rust Ethereum dev stack), Mythril (symbolic execution), Slither (static analysis), Echidna (property testing), formal verification (K framework, Certora).
