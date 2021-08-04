# Breadth-First Search
- Simple algorithm for searching a graph.
- Prim's minimum-spanning-tree algorithm.
- Dijkstra's single-source shortest-paths algorithm.
- Given a graph *G* = (*V*, *E*) and a **source** vertex *s*, breadth-first search explores the edges of *G* to "discover" every vertex that is reachable from *s*.
- Computes distance (smallest number of edges) from *s* to each reachable vertex.
- Produces a "breadth-first tree" with root *s* that contains all reachable vertices.
- For any vertex *v* reachable from *s*, the simple path in the breadth-first tree from *s* to *v* corresponds to a "shortest path" from *s* to *v* in *G*.
- Works on directed and undirected graphs.
- Algorithm discovers all vertices at distance *k* from *s* before discovering any vertices at distance *k* + 1.

## Pseudocode
```
BFS(G,s)
1.  for each vertex u ∈ G.V - {s}
2.      u.color = WHITE
3.      u.d = ∞
4.      u.π = NIL
5.  s.color = GRAY
6.  s.d = 0
7.  s.π = NIL
8.  Q = ∅
9.  ENQUEUE(Q,s)
10. while Q ≠ ∅
11.     u = DEQUEUE(Q)
12.     for each v ∈ G.Adj[u]
13.         if v.color == WHITE
14.             v.color = GRAY
15.             v.d = u.d + 1
16.             v.π = u
17.             ENQUEUE(Q,v)
18.     u.color = BLACK
```

- Uses adjacency list above.
- Store color of each vertex u ∈ V in the attribute u.color and parent of u in the attribute u.π.
- u.d holds the distance from the source *s* to vertex *u*.
- Algorithm uses a FIFO queue *Q* to manage set of vertices.

- Below illustrates BFS on a sample graph.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bfs_process.png "Graph of BFS on a sample graph")

## Analysis
- The operations of enqueuing and dequeuing take O(1) time.
- Total time devoted to queue operations is O(V).
- Scans each adjacency list at most once.
- Total time spent ins scanning adjacency lists is O(E) because the length of all adjacency lists is &Theta;(E).
- Overhead for initialization is O(V).
- Total running time of BFS procedure is O(V + E).
- BFS runs in time linear in the size of the adjacency-list representation of *G*.

## Shortest Paths
- Define the **shortest-path distance** &delta;(s,v) from *s* to *v* as the minimum number of edges in any path from vertex *s* to vertex *v*.
- If there is no path from *s* to *v*, then &delta;(s,v) = ∞.
