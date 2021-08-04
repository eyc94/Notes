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
