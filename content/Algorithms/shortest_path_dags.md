# Single-Source Shortest Paths in Directed Acyclic Graphs
- We can compute shortest paths from a single source in &Theta;(V + E) time.
- Algorithm starts by topologically sorting the dag to make a linear ordering on vertices.
- If there is a path from *u* to *v*, then *u* comes before *v* in the topological sort.
- Just make one pass over vertices in topologically sorted order.
- After processing vertex, we relax each edge that leaves the vertex.

## Pseudocode

```
DAG-SHORTEST-PATHS(G,w,s)
1.  topologically sort the vertices of G
2.  INITIALIZE-SINGLE-SOURCE(G,s)
3.  for each vertex u, taken in topologically sorted order
4.      for each vertex v ∈ G.Adj[u]
5.          RELAX(u,v,w)
```

- Running time of algorithm:
    - Topological sort of line 1 takes &Theta;(V + E) time.
    - INITIALIZE-SINGLE-SOURCE in line 2 takes &Theta;(V) time.
    - The for loop of lines 3-5 makes one interation per vertex.
    - The for loop of lines 4-5 relaxes each edge exactly once.
    - Each iteration of the inner for loop takes &Theta;(1) time.
    - Total running time is &Theta;(V + E).

![alt text](https://github.com/eyc94/Notes/blob/master/images/dag_shortest_path_example.png "Image of an example of shortest path on dag")