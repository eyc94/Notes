# Graphs
- Similar to trees.
- Can have cycles.
- Two ways to search for things in graphs:
    - Breadth First Search (BFS)
    - Depth First Search (DFS)
- Dijkstra's Algorithm
    - Shortest path from one node to another.
- Made of vertices and edges

## Graph Components
- Vertices are objects, states, locations, etc.
- Forms a set where each vertex is unique.
    - V = {v<sub>1</sub>, v<sub>2</sub>, v<sub>3</sub>, ..., v<sub>n</sub>}
-Edges represent relationships between vertices.
    - E = {(v<sub>i</sub>, v<sub>j</sub>), ...}
    - Directed or undirected.
    - If there is an edge between v<sub>i</sub> and v<sub>j</sub>, v<sub>i</sub> and v<sub>j</sub> are adjacent vertices.
    - Weighted or unweighted.

## Representing Graphs
- **Adjaceny List**: Each vertex stores a list of its adjacent vertices.
- **Adjacency Matrix**: Two dimensional matrix whose rows and columns represent vertices. If there is an edge between v<sub>i</sub> and v<sub>j</sub>, the value at location (i, j) will be non-zero.
- Space complexity:
    - Adjacency List: *O(|V| + |E|)*
    - Adjacency Matrix: *O(|V|<sup>2</sup>)*