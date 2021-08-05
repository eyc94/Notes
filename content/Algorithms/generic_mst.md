# Generic Minimum Spanning Tree
- Grows minimum spanning tree one edge at a time.
- Manages a set of edges *A* following the invariant:
    - Prior to each iteration, *A* is a subset of some minimum spanning tree.
- At every step, we determine an edge that we can add to *A* safely without violating the invariant.
- We call this edge a **safe edge**.

## Pseudocode

```
GENERIC-MST(G,w)
1.  A = ∅
2.  while A does not form a spanning tree
3.      find an edge (u,v) that is safe for A
4.      A = A U {(u,v)}
5.  return A
```

- When line 3 is executed, we know that there is a spanning tree *T*.
- There is a subset *A* of *T*.
- There is an edge that is in *T* that is not yet in *A*.
- Determine that this edge is safe and then add to *A*.


## Theorem for Determining Safe Edges

![alt text](https://github.com/eyc94/Notes/blob/master/images/partition_example.png "Image of partition of a graph")
- First, we need some definitions.
    - A **cut** (S,V - S) of an undirected graph is a partition of V.
    - An edge **crosses** the cut if one endpoint is in *S* and the other in *V* - *S*.
    - A cut **respects** a set *A* of edges if no edge in *A* crosses the cut.
    - An edge is a **light edge** crossing a cut if its weight is the minimum of any edge crossing the cut.
- Rule for determining safe edges:
    - Let *G* = (*V*,*E*) be a connected, undirected graph. *A* is a subset of *E* that is included in some minimum spanning tree for *G*. Let (*S*,*V* - *S*) be any cut of *G* that respects *A*. Let (u,v) be a light edge crossing the cut. Then edge (u,v) is safe for *A*.