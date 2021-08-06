# Dijkstra's Algorithm
- Solves single-source shortest-paths problem on a weight, directed graph *G* for the case in which all edge weights are nonnegative.
- Assume weight of each edge is positive.
- Maintains a set *S* of vertices whose final shortest-path weights from source have been determined.
- Algorithm selects vertex u in V - S with the minimum shortest-path estimate and adds it to S and relaxes edges leaving u.
- We use a min-priority queue Q of vertices.

## Pseudocode

```
DIJKSTRA(G,w,s)
1.  INITIALIZE-SINGLE-SOURCE(G,s)
2.  S = ∅
3.  Q = G.V
4.  while Q ≠ ∅
5.      u = EXTRACT-MIN(Q)
6.      S = S U {u}
7.      for each vertex v ∈ G.Adj[u]
8.          RELAX(u,v,w)
```

- Line 1 initializes the *d* and π values in the usual way.
- Line 2 initializes the set *S* to empty.
- Maintains the invariant that Q = V - S at the start of each iteration of the while loop of lines 4-8.
- Line 3 initializes the min-priority queue Q to contain all vertices in V.
- Each time through the while loop of lines 4-8, line 5 extracts a vertex u from Q = V - S and line 6 adds it to set *S*.
- Line 7-8 relax each edge (u,v) leaving u, thus updating the estimate v.d and the predecessor v.π if we can improve the shortest path to v found so far by going through u.

![alt text](https://github.com/eyc94/Notes/blob/master/images/dijkstra_example.png "Image of an example of dijkstra's algorithm")