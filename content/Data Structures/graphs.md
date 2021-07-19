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

#### Depth-First Search and Breadth-First Search
- Above example was DFS.
- DFS explores as far as possible before trying another path.
- DFS can be implemented using a stack
- If we replace the stack with a queue, it results in a BFS.
- BFS explores a tree by traveling all paths to a given depth, then traveling all those paths one step deeper, then traveling them one step deeper, etc.
- BFS visits neighbors before going down.
- General algorithm for DFS and BFS below. For DFS, use stack. For BFS, use queue.

```
1. Initialize an empty set of visited vertices.
2. Initialize an empty stack (DFS) or queue (BFS). Add v<sub>i</sub> to the stack/queue.
3. If the stack/queue is not empty, pop/dequeue a vertex v.
4. Perform any desired processing on v.
    - e.g. Check if v meets a desired condition.
5. (DFS only): If v is not in the set of visited vertices:
    - Add v to the set of visited vertices.
    - Push each vertex that is direct successor of v to the stack.
6. (BFS only):
    - Add v to the set of visited vertices.
    - For each direct successor v' of v:
        - If v' is not in the set of visited vertices, enqueue it into the queue.
7. Repeat from 3.
```

- Both can be used to find start to finish in a maze.
- Comparisons between DFS and BFS:
    - DFS is backtracking search.
    - In an infinite graph, DFS gets lost in an infinite path and won't find a solution.
    - BFS is complete and optimal. If a solution exists, BFS is guaranteed to find it, and it will find the shortest path to that solution.
    - BFS may take a long time if solution is deep in graph.
    - DFS may find a deep solution more quickly.
    - Both algorithms have **O(V)** space complexity in worst case.
    - BFS may take more space in practice, however.
    - If graph has a high branching factor, BFS can take a lot of memory to maintain all of the paths.

#### Dijkstra's Algorithm: Single Source Lowest-Cost Paths
- Finds the shortest/lowest-cost path from a specified vertex in a graph to all other reachable vertices in the graph.
- From airports graph, you can also find the cheapest cost to reach each of the airports.
- Structured like DFS and BFS. However, use priority queue.
    - Priority values used in queue correspond to the cumulative distance to each vertex added to the PQ.
    - We are always exploring the remaining node with the minimum cumulative cost.
- Algorithm which begins with some source vertex v<sub>s</sub>.
    - Initialize empty map/hash table representing visited vertices.
        - Key is the vertex *v*.
        - Value is the min distance *d* to vertex *v*.
    - Initialize an empty PQ, and insert *v<sub>s</sub>* with distance (priority) 0.
    - While PQ is not empty:
        - Remove first element (a vertex) from the PQ and assign it to *v*.
        - Let *d* be *v*'s distance (priority).
        - If *v* is not in the map of visited vertices:
            - Add *v* to the visited map with distance/cost *d*.
            - For each direct successor *v<sub>i</sub>* of *v*:
                - Let *d<sub>i</sub>* equal the cost/distance associated with edge *(v, v<sub>i</sub>)*.
                - Insert *v<sub>i</sub>* to the PQ with distance (priority) *d + d<sub>i</sub>*.

- This version only keeps track of the min distance to each vertex, but it can be easily modified to keep track of the min-distance path, too.
    - Do this by augmenting visited vertex map and the PQ to keep track of the vertex previous to each one added.

- Complexity of this version is **O(|E| log |E|)**.
- Inner loop executed at most |E| times.
- Cost of the instructions inside the loop is **O(log |E|)**.
- Inner cost comes from inserting into the PQ.
