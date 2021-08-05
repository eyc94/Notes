# Minimum Spanning Trees
- We have an electronic circuit design with pins that need wiring.
- There are *n* pins. This means we need to use *n* - 1 wires.
- We need an arrangement of pins that use the least amount of wire.
- Model wiring problem with a connected, undirected graph G = (V, E), where V is the set of pins, E is the set of possible interconnections between pairs of pins.
- We have a weight for each edge (amount of wire needed) to connect u and v.
- We want to find a subset of the edges in which they connect all vertices and has the least total weight.
- This subset is acyclic and connects all vertices, so it forms a tree.
- This tree is called a **spanning tree** since it "spans" the graph G.
- Determining the tree T is the **minimum-spanning-tree problem**.
- There are two algorithms for solving this problem:
    1. Kruskal's algorithm.
    2. Prim's algorithm.
- They run in O(E lg V) time using ordinary binary heaps.
- Using Fibonacci heaps, Prim's algorithm runs in time O(E + V lg V), which improves over the binary heap implementation if |V| is much smaller than |E|.
- Both algorithms are greedy.

![alt text](https://github.com/eyc94/Notes/blob/master/images/mst_example.png "Image of an example of a minimimum spanning tree of a graph")