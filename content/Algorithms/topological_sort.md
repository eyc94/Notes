# Topological Sort
- Use depth-first search to perform a topological sort of a directed acyclic graph, or a "dag".
- A **topological sort** of a dag *G* = (*V*,*E*) is a linear ordering of all its vertices such that if *G* contains an edge (*u*,*v*), then *u* appears before *v* in the ordering.
- If graph has a cycle, no linear ordering is possible.
- Topological sort of a graph is an ordering of vertices along a horizontal line so that all directed edges go from left to right.

![alt text](https://github.com/eyc94/Notes/blob/master/images/topological_sort_example.png "Image of a topological sort")

- This is an example of how getting ready in the morning can be represented as such.
- We must wear socks before shoes.
- Other items can be put on in any order (like socks and pants).
- Gives ordering for getting dressed.

## Pseudocode

```
TOPOLOGICAL-SORT(G)
1.  call DFS(G) to compute finishing times v.f for each vertex v
2.  as each vertex is finished, insert it onto the front of a linked list
3.  return the linked list of vertices
```

- Runtime: &Theta;(V + E) because DFS takes &Theta;(V + E) time and it takes O(1) time to insert each of the |V| vertices onto the front of the linked list.