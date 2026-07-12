# EVM

## Scope
The Ethereum Virtual Machine: bytecode, opcodes, gas mechanics, execution model, and state management.

## Core principles
- The EVM is a stack-based VM (not register-based): operations push/pop values on a 1024-slot stack; memory is linear and byte-addressable.
- Gas is compute budgeting: each opcode costs gas (PUSH=3, ADD=3, SSTORE=20k for new storage slots); a transaction dies if it runs out, wasting all gas but not side-effects.
- State (accounts, balances, nonces, code, storage) is a Merkle Patricia tree; state transitions are atomic (all-or-nothing within a transaction).
- Call depth is limited to 1024 (to prevent stack explosions); calls at depth 1024 fail, breaking assumptions in recursive patterns.
- Gas refunds are limited to 50% of gas spent (EIP-3529); optimizations exploiting refunds (storage deallocation, selfdestruct) have diminishing returns.

## Apex practices
- Optimize for gas: minimize SSTORE (most expensive opcode), cache values in memory (cheaper), batch writes (storage is per-slot, not per-byte).
- Use YUL (Ethereum's inline assembly language) for low-level optimizations; Solidity compiles to YUL then bytecode.
- Gas estimations are heuristic; test on testnets with real gas prices and account for variations (MEV, transaction batching).
- Memory layout matters: Solidity arranges storage slots predictably; packed storage (multiple bool/uint8 per slot) saves gas but increases bytecode complexity.

## Pitfalls
- Assuming high call depth won't happen; distributed systems (wrapped tokens, proxy chains) can exceed depth 1024.
- Gas refunds disappearing (EIP-3529 cut them in half, some opcodes were repriced); old gas-optimization techniques no longer work.
- State transitions that assume atomicity but include external calls; a reentrancy during the call can fork the state mid-transaction.

## Tools & references
Ethereum Yellow Paper (state transition spec), EIP (Ethereum Improvement Proposals), solc (Solidity compiler), evm.codes (opcode reference), gas optimization guides (Uniswap, dYdX), Echidna (EVM property testing).
