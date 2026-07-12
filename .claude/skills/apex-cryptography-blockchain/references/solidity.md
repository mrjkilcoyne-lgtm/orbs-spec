# Solidity

## Scope
Ethereum's smart contract language: syntax, type system, common pitfalls, security patterns, and best practices.

## Core principles
- Solidity is dynamically typed in some ways (type casting allowed, implicit conversions) — this is dangerous; always be explicit about types and use checked arithmetic (Solidity 0.8+).
- Visibility (private, internal, public, external) defines what can be called; private doesn't mean secret (all data on blockchain is public), it means not callable from outside.
- Modifiers are macros that inject code; they're used for access control (onlyOwner) and guards (checks-effects-interactions).
- Events are efficient logs (indexed for querying off-chain) but not storage; contracts cannot read past events, and events do not state changes.
- Inheritance linearization (C3 linearization) determines the order of contract initialization; mistakes lead to unexpected state and bypassed checks.

## Apex practices
- Use OpenZeppelin's Ownable (access control), ReentrancyGuard (reentrancy defense), and ERC-20/721 implementations as baselines.
- Declare visibility explicitly for all functions and state variables (Solidity 0.5+ requires this); avoid fallback functions and delegatecall unless necessary.
- Test state changes exhaustively: each branch, each state transition, and the interaction between multiple contracts.
- Upgrade using proxy patterns (UUPS, transparent proxy) only for complex systems; simpler contracts should be replaced with new deployments and migration.

## Pitfalls
- Integer overflow/underflow before Solidity 0.8 (now reverts automatically); libraries like SafeMath are now redundant.
- Delegatecall used with untrusted code; it executes in the caller's context, so malicious code can mutate state.
- Front-running (MEV): a transaction waiting in the mempool can be reordered or inserted by miners/validators; mitigate with commit-reveal or MEV-resistant designs.

## Tools & references
Solidity documentation, OpenZeppelin Contracts, Hardhat (testing), Foundry (Rust-based Ethereum dev stack), Slither (static analysis), Mythril (symbolic execution), Solhint (linter).
