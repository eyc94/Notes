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

## Working With Graphs
- Can we get from node A to node B?
- Fastest path?

#### Single Source Reachability
- What nodes are reachable from a specific node?
- Use the steps below to find reachable vertices from some vertex v<sub>i</sub>:
    1. Initialize an empty set of reachable vertices.
    2. Initialize an empty stack.
    3. Add v<sub>i</sub> to the stack.
    4. If the stack is not empty, pop a vertex v from the stack.
    5. If v is not in the set of reachable vertices:
        - Add it to the set of reachable vertices.
        - Add each vertex that is direct successor of v to the stack.
    6. Repeat from 3.

![alt text](https://github.com/eyc94/Notes/blob/master/images/airports_graph_directed.png "Image of a directed airport graph")

- Look for reachable airports from PDX:

```
reachable: {}
stack: [PDX]

v: PDX
successors: [SEA, SFO]
reachable: {PDX}
stack: [SEA, SFO]

v: SFO
successors: [ORD, PDX]
reachable: {PDX, SFO}
stack: [SEA, ORD, PDX]

v: PDX (already reachable)
successors: - -
reachable: {PDX, SFO}
stack: [SEA, ORD]

v: ORD
successors: [MSP, STL]
reachable: {ORD, PDX, SFO}
stack: [SEA, MSP, STL]

v: STL
successors: [LAX, ORD]
reachable: {ORD, PDX, SFO, STL}
stack: [SEA, MSP, LAX, ORD]

v: ORD (already reachable)
successors: - -
reachable: {ORD, PDX, SFO, STL}
stack: [SEA, MSP, LAX]

v: LAX
successors: [ORD, SFO]
reachable: {LAX, ORD, PDX, SFO, STL}
stack: [SEA, MSP, ORD, SFO]

v: SFO, ORD (already reachable)
successors: - -
reachable: {LAX, ORD, PDX, SFO, STL}
stack: [SEA, MSP]

v: MSP
successors: [PDX, SFO]
reachable: {LAX, MSP, ORD, PDX, SFO, STL}
stack: [SEA, PDX, SFO]

v: SFO, PDX (already reachable)
successors: - -
reachable: {LAX, MSP, ORD, PDX, SFO, STL}
stack: [SEA]

v: SEA
successors: [MSP, PDX]
reachable: {LAX, MSP, ORD, PDX, SEA, SFO, STL}
stack: [MSP, PDX]

v: PDX, MSP (already reachable)
successors: - -
reachable: {LAX, MSP, ORD, PDX, SEA, SFO, STL}
stack: []

Done (empty stack)
reachable: {LAX, MSP, ORD, PDX, SEA, SFO, STL}
```

- Can be implemented by adjacency list or adjacency matrix.
- Could use a queue instead of a stack.