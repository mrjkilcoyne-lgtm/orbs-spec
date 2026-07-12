# Chain Indexing

## Scope
Indexing on-chain data for efficient queries: subgraphs (The Graph), data lakes, and real-time event streaming.

## Core principles
- Blockchains are write-heavy, query-slow: reading state from a chain requires syncing and querying raw state, which is inefficient; indexing extracts events and state into queryable databases.
- Event indexing captures Solidity events (emitted during transaction execution) and decodes them into structured data; events are the primary source of truth for off-chain data.
- State snapshots (periodic copies of contract state) enable efficient time-travel queries; reconstructing state at block 100 from scratch is slow, but snapshots plus diffs are fast.
- Subgraphs (The Graph) define entities, fields, and data sources; they sync with the chain, decode events, and serve GraphQL queries.
- Materialized views (pre-computed aggregates like "total TVL" or "daily volume") reduce query latency; they're updated incrementally as new blocks arrive.

## Apex practices
- Use The Graph for public chains and standard token/NFT data; hosted service (free) or self-hosted graph-node for more control.
- Define subgraph schemas carefully (entity relationships, indexed fields); bad schemas lead to slow queries or incorrect data.
- Index events, not storage reads; storage reads are slow on-chain and expensive to index, while events are efficient.
- Monitor indexing lag (how far behind the head block is the indexer?); if lag > 1 block, queries may return stale data.

## Pitfalls
- Subgraph bugs (incorrect event decoding, wrong entity relationships) lead to silent data corruption; test queries against known data.
- Indexing full state history is expensive (storage, query time); decide what data is queryable and accept that old data may be archived.
- Graph node crashes or reorgs (chain forks cause blocks to be rewritten) require re-indexing; plan for recovery and backup indexers.

## Tools & references
The Graph (hosted service, decentralized network), graph-node (implementation), Subgraph Studio (development), GraphQL (query language), Substreams (streaming indexing), Elasticsearch (alternative for full-text search), Dune Analytics (data warehouse), Blockchain.com (on-chain data provider).
