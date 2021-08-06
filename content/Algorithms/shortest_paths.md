# Single-Source Shortest Paths
- Finding the shortest path from city to city is an example.
- BFS is a shortest-paths algorithm that works on unweighted graphs (unit weight).
- We want to focus on the **single-source shortest-paths problem**:
    - Given a graph *G*, we want to find a shortest path from a given **source** vertex *s* to each vertex *v*.

## Optimal Substructure of a Shortest Path
- Shortest paths between two vertices contain other shortest paths within it.
- Dijkstra's algorithm is greedy.

## Negative-Weight Edges
