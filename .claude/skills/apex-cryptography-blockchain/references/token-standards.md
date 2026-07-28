# Token Standards

## Scope
ERC standards for tokens on Ethereum: fungible (ERC-20), non-fungible (ERC-721), multi-token (ERC-1155), and custom token mechanics.

## Core principles
- ERC-20 is the standard for fungible tokens (all units equivalent): balanceOf, transfer, approve+transferFrom allow delegation.
- The approve/transferFrom pattern (pull model) is safer than transfer-then-delegate (push model) but creates a two-step UX for spending allowances.
- ERC-721 is for non-fungible tokens (unique items): each token has an ID and owner; ownership is easily queryable and tradeable.
- ERC-1155 (multi-token) allows one contract to manage multiple token types (fungible and non-fungible), reducing contract deployments.
- Permit (EIP-2612) allows approval via signature instead of two transactions, but requires careful implementation to avoid replay attacks.

## Apex practices
- Use OpenZeppelin's ERC20, ERC721, ERC1155 implementations; they handle standard edge cases and are battle-tested.
- Implement safeTransferFrom for NFTs (ERC-721 receiver pattern) to prevent tokens being sent to contracts that can't handle them.
- Permit extensions (EIP-2612) are valuable for UX but require DOMAIN_SEPARATOR (chain ID + contract address + salt) for replay prevention.
- Custom token mechanics (mintable, burnable, taxable) should be clear in documentation; surprises (hidden taxing on transfer) break composability.

## Pitfalls
- ERC-20 approve-then-transfer creates a race condition: if an approver revokes allowance by calling approve(0), a pending transferFrom could be replaced by the recipient calling approve with more.
- Non-standard ERC-20 implementations (returning no value, throwing on approval failure) break many contracts; use OpenZeppelin for compatibility.
- NFTs without receiver hooks can be permanently lost if sent to a contract that doesn't implement IERC721Receiver.

## Tools & references
EIP-20 (ERC-20 standard), EIP-721 (ERC-721 standard), EIP-1155 (ERC-1155 multi-token), EIP-2612 (permit), OpenZeppelin Contracts, Token Lab (test suite).
