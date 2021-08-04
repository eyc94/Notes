# Depth-First Search
- Search deeper in the graph whenever possible.
- Explores edges of the most recently discovered vertex *v* that still has unexplored edges.
- Once all *v*'s edges are explored, the search backtracks to explore edges leaving the vertex from which *v* was discovered.

## Pseudocode
```
DFS(G)
1.  for each vertex u ∈ G.V
2.      u.color = WHITE
3.      u.π = NIL
4.  time = 0
5.  for each vertex u ∈ G.V
6.      if u.color == WHITE
7.          DFS-VISIT(G,u)
```

```
DFS-VISIT(G,u)
1.  time = time + 1             // White vertex u has just been discovered
2.  u.d = time
3.  u.color = GRAY
4.  for each v ∈ G.Adj[u]       // Explore edge (u,v)
5.      if v.color == WHITE
6.          v.π = u
7.          DFS-VISIT(G,v)
8.  u.color = BLACK             // Blacken u; it is finished
9.  time = time + 1
10. u.f = time
```

- Illustration of the use of DFS.
![alt text](https://github.com/eyc94/Notes/blob/master/images/dfs_process.png "Graph of DFS on a sample graph")

- Running time: &Theta;(V + E)