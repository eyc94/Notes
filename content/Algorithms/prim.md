# Prim's Algorithm
- Elaborates on generic method.
- Uses a specific rule to determine a safe edge in line 3 of the generic method.
- The set *A* forms a single tree. The safe edge added to *A* is always a least-weight edge connecting the tree to a vertex not in the tree.
- Operates like Dijkstra's algorithm.
- Edges in the set *A* always form a single tree.

![alt text](https://github.com/eyc94/Notes/blob/master/images/prim_example.png "Image of example of Prim's algorithm")

- Tree starts from an arbitrary root vertex *r* and grows until the tree spans all the vertices in *V*.
- Each step adds to the tree *A* a light edge that connects *A* to an isolated vertex - one on which no edge of *A* is incident.
- Strategy is greedy because at each step it adds to the tree an edge that contributes the minimum amount possible to the tree's weight.

## Pseudocode
- Need a fast way to select a new edge to add to the tree formed by the edges in *A*.

```
MST-PRIM(G,w,r)
1.  for each u ∈ G.V
2.      u.key = ∞
3.      u.π = NIL
4.  r.key = 0
5.  Q = G.V
6.  while Q ≠ ∅
7.      u = EXTRACT-MIN(Q)
8.      for each v ∈ G.Adj[u]
9.          if v ∈ Q and w(u,v) < v.key
10.             v.π = u
11.             v.key = w(u,v)
```

- Lines 1-5 set the key of each vertex to ∞ (except for the root *r*, whose key is set to 0 so that it will be the first vertex processed). Set the parent of each vertex to NIL. Initialize the min-priority queue *Q* to contain all the vertices.
- Algorithm maintains the following three-part loop invariant:
    1. A = {(v,v.π):v ∈ V - {r} - Q}.
    2. The vertices already placed into the minimum spanning tree are those in V - Q.
    3. For all vertices v ∈ Q, if v.π ≠ NIL, then v.key < ∞ and v.key is the weight of a light edge (v,v.π) connecting *v* to some vertex already placed into the minimum spanning tree.
- Line 7 identifies a vertex u ∈ Q incident on a light edge that crosses the cut (V - Q,Q).
- For loop of lines 8-11 updates the key and π attributes of every vertex *v* adjacent to *u* but not in the tree, thereby maintaining the third part of the loop invariant.
- Running time: O(E lg V).
- Using fibonacci heaps, runtime is: O(E + V lg V).