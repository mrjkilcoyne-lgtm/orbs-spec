# Graph Databases

## Scope
Storing and querying highly connected data (nodes, edges, properties). Graph traversals (depth-first, breadth-first, pattern matching). Neo4j, Amazon Neptune, and graph query languages (Cypher, Gremlin).

## Core principles
- Graphs are optimized for traversals (friends of friends, recommendation chains, dependency discovery). Each edge is indexed, so "all neighbors of node X" is O(degree), not O(all edges). Relational databases require expensive joins for deep traversals.
- Property graphs have labeled nodes and edges with attributes: nodes are entities (User, Product), edges are relationships (FOLLOWS, PURCHASED) with properties (timestamp, rating). This is richer than simple graphs.
- Graph queries express patterns (e.g., "users who follow users that bought this product") declaratively. Cypher (Neo4j) and Gremlin (TinkerPop) are graph query languages; both avoid impedance mismatch with SQL.
- Graph traversals have variable depth (friends within distance 3) and can aggregate along paths (sum of transaction amounts along a chain). This is awkward in SQL; it's natural in graph databases.
- Scaling graphs is hard: partitioning by node ID (sharding) breaks edges that cross partitions. Graph databases struggle with large-scale distributed queries; single-machine or federation models are common.

## Apex practices
- Use graphs for highly connected queries: recommendation systems, fraud detection (money trails), access control (who can see what), and knowledge graphs. Don't use graphs for bulk analytics (Spark is cheaper).
- Design the graph schema (node types, edge types, properties) with query patterns in mind. If most queries start from users, index by user. If most queries traverse through products, cluster products together.
- Cache frequently traversed paths or aggregated results (e.g., "friends count") in a separate property to avoid expensive re-traversal.
- Use APOC (Awesome Procedures On Cypher) library (Neo4j) or custom Gremlin steps to express complex patterns. Avoid recursive queries in application code.

## Pitfalls
- Over-modeling the domain as a graph when a relational or document model is simpler (not every many-to-many needs a graph database).
- Storing immutable historical data in a mutable graph, making audit trails impossible; use temporal properties or versioned nodes instead.
- Not setting cache sizes and memory appropriately; Neo4j's page cache can fill available RAM and cause thrashing.

## Tools & references
Neo4j documentation (Cypher, architecture, tuning), Apache TinkerPop (Gremlin), Amazon Neptune, "Graph Algorithms" (Hamilton), "Learning Neo4j" (Webber, et al.), APOC library.
