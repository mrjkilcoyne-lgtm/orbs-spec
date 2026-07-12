# Graph Theory

## Scope
Fundamental structures and algorithms: paths, cycles, connectivity, shortest paths, spanning trees, and maximum flow; applications to networks and optimization.

## Core principles
- Graphs formalize relationships: nodes and edges encode structure (social networks, dependency graphs, road maps). Directed vs. undirected and weighted vs. unweighted capture different problem types.
- Connectivity (is there a path?) is answered by BFS/DFS in O(V+E) time; tree structure (acyclic connected graph) is the minimal connected structure.
- Shortest paths: BFS for unit weights (O(V+E)), Dijkstra for non-negative weights (O((V+E)logV)), Bellman-Ford for negative weights (O(VE)); choose by constraints.
- Maximum flow and minimum cut are dual: flow conservation (in = out except source/sink) and cut minimality (smallest set of edges separating source/sink) solve the same dual problem.
- Strongly connected components (directed graphs) partition nodes into groups reachable from each other; DAGs of SCCs enable topological sorting and dynamic programming.

## Apex practices
- Use adjacency lists for sparse graphs (most real-world), adjacency matrices for dense or small graphs; choice affects algorithm complexity.
- Topological sorting (via DFS) on DAGs unlocks dynamic programming solutions; many optimization problems reduce to DAG shortest paths.
- Flow algorithms (Ford-Fulkerson with DFS/BFS, Edmonds-Karp with BFS, push-relabel) scale differently; use Edmonds-Karp or better for production.
- Model resource constraints, matchings, and routing as network flow problems; it's often easier than designing custom algorithms.

## Pitfalls
- Ignoring cycles in directed graphs; a cycle has no topological order and breaks algorithms assuming DAG structure.
- Confusing shortest path with minimum spanning tree; shortest path is point-to-point, MST connects all nodes with minimum total weight.
- Forgetting that Dijkstra fails on negative weights; use Bellman-Ford instead (slower but correct).

## Tools & references
Cormen et al.'s "Introduction to Algorithms," NetworkX (Python), LEMON (C++), Ahuja-Magnanti-Orlin on network flow.
