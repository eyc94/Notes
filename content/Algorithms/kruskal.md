# Kruskal's Algorithm
- Elaborates on the generic method.
- Uses a specific rule to determine a safe edge in line 3 of the generic method.
- The set *A* is a forest whose vertices are all those of the given graph. Safe edge added to *A* is always a least-weight edge in the graph that connects two distinct components.

## Pseudocode
- Finds safe edge of least weight that connects any two trees in the forest.
- Greedy algorithm because it looks for an edge of least possible weight at each step.
```
MST-KRUSKAL(G,w)
1.  A = ∅
2.  for each vertex v ∈ G.V
3.      MAKE-SET(v)
4.  sort the edges of G.E into nondecreasing order by weight w
5.  for each edge (u,v) ∈ G.E, taken in nondecreasing order by weight
6.      if FIND-SET(u) ≠ FIND-SET(v)
7.          A = A U {(u,v)}
8.          UNION(u,v)
9.  return A
```
- Lines 1-3 initialize the set *A* to empty set and create |V| trees (one for each vertex).
- Lines 5-8 examines edges in order of weight, from low to high.
- The loop checks each edge (u,v) to see if the endpoints u and v are in the same tree.
    - If they are, discard the edge.
    - If not, they belong to two different trees. Line 7 adds the edge to *A*. Line 8 merges the vertices in the two trees.
- Below is a picture:

![alt text](https://github.com/eyc94/Notes/blob/master/images/kruskal_example_one.png "Image of an example of kruskal's algorithm")
![alt text](https://github.com/eyc94/Notes/blob/master/images/kruskal_example_two.png "Image of an example of kruskal's algorithm")