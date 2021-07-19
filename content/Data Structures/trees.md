# Trees

## Introduction
- Trees start at roots that branch to 0 or more nodes until you reach the end node (a leaf).
- There are Binary Trees where every node has at most 2 child nodes.
- There are Binary Search Trees (BSTs) that have special properties.
    - All values to the left of the node are smaller.
    - All values to the right of the node are larger or equal to.
    - The "equal to" condition can be on the left or right side.

## General Trees
- Elements represented as nodes.
- Nodes contain data and a reference to another node.
- Relationship between nodes is an edge or an arc.
- Edges represent directed relationships.

![alt text](https://github.com/eyc94/Notes/blob/master/images/general_tree.png "Image of general tree")

## Definitions
- Parent: A node P in a tree is called the parent of another node C if P has an edge that points directly to C.
    - Node B is the parent of nodes E and F.
- Child: A node C in a tree is the child of another node P if P is C's parent.
    - Nodes E and F are the children of node B.
- Sibling: A node S1 is a sibling of another node S2 if they both share the same parent node P.
    - Nodes B, C, and D are siblings.
- Descendant: The descendant of node N are all of N's children, plus its children's children, and so forth.
    - Nodes F, E, and I are descendants of node B.
- Ancestor: A node A is the ancestor of another node D if D is a descendant of A.
    - Node B is the ancestor of nodes E, F, and I.
- Root: The ancestor of all nodes in a tree.
    - Node A
- Interior Node: A node in a tree is an interior node if it has at least one child.
    - Nodes A, B, C, D, E, G, H are interior nodes.
- Leaf Node: A node is a leaf node if it has no children.
    - Nodes F, I, J, K, and L.
- Subtree: The portion of a tree that contains a single node N, N's descendants, and the edges joining these nodes.
    - Call this the subtree rooted at N.
    - The subtree rooted at node C has the nodes C, G, J, and K.
- Path: Collection of edges in a tree joining a node to its descendants.
- Path Length: The length of a path in a tree is the number of edges in that path.
    - Path from node C to node K is 2 because it has 2 edges.
- Depth: Depth of a node N is the length of the path from the root to that node N.
    - Root node has depth of 0.
    - Depth of node K is 3.
- Height: Maximum depth of any node in the tree.
    - Height is 3.

## Constraints
- Each node has only one parent.
- Edges may not form cycles.