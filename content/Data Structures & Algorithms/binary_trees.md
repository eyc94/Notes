# Binary Trees

## Introduction
- Each node in a tree can have at most two children.
    - These nodes are labeled as left child and right child.
- We can talk about a node's left subtree as the subtree rooted at that node's left child.
- We can talk about a node's right subtree as the subtree rooted at that node's right child.

![alt text](https://github.com/eyc94/Notes/blob/master/images/binary_tree.png "Image of Binary Tree")

## States of Binary Trees

#### Full Binary Tree
- Every interior node has exactly two children.

![alt text](https://github.com/eyc94/Notes/blob/master/images/full_binary_tree.png "Image of Full Binary Tree")

#### Perfect Binary Tree
- A Full Binary Tree where all the leaves are at the same depth.
- If the tree has height h:
    - It has *2<sup>h</sup>* leaves.
    - It has *2<sup>h+1</sup>* - 1 total nodes.
- If the tree has *n* nodes, then the height is approximately *log(n)*.

![alt text](https://github.com/eyc94/Notes/blob/master/images/perfect_binary_tree.png "Image of Perfect Binary Tree")

#### Complete Binary Tree
- A Complete Binary Tree is perfect except for the deepest level, whose nodes are as far left as possible.

![alt text](https://github.com/eyc94/Notes/blob/master/images/complete_binary_tree.png "Image of Complete Binary Tree")

## Binary Search Trees
- The key of each node N is greater than all the keys in N's left subtree and less than or equal to all the keys in N's right subtree.
- It does not have to be full, complete, or perfect.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst.png "Image of Binary Search Tree")

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst_example.png "Example of Binary Search Tree")

## Traversals
- We use tree traversals to process nodes in our tree in a certain order.
- There are 2 types of tree traversals:
    - Depth-first: Explores a tree subtree by subtree, visiting all of a node's descendants before visiting any of its siblings (and their descendants). Moves as far down in the tree as it can go before moving across in the tree.
    - Breadth-first: Explores a tree level by level. It visits every node at a given depth before moving downward and traversing the nodes at the next-deepest level. Moves far across the tree before moving down in the tree.

#### Depth First Traversal
- Move downward in tree as far as possible before moving across.
- There are several kinds of depth-first BST traversals. We look at three kinds and use the letters N, L, and R.
    - N: Visit/process the current node itself.
    - L: Traverse the left subtree of the current node.
    - R: Traverse the right subtree of the current node.
- Each depth-first BST traversal does these 3 things but in different orders.
    - Pre-Order Traversal: NLR - Process the current node before traversing the left and right subtrees.
    - In-Order Traversal: LNR - Traverse the left subtree before processing the node. Then traverse the right subtree.
    - Post-Order Traversal: LRN - Traverse both the left and right subtrees. Process the current node.
- Visualize using the picture below:
    - Think of walking on the dotted lines.
    - The walk encounters each node exactly 3 times
        - 1) Before walking the subtrees. Left of node. **Pre-Order Traversal**
        - 2) After walking the left subtree. Bottom of node. **In-Order Traversal**
        - 3) After walking the right subtree. Right of node. **Post-Order Traversal**
    - Pre-Order: 64, 32, 16, 48, 56, 80, 72, 88, 84, 96.
    - In-Order: 16, 32, 48, 56, 64, 72, 80, 84, 88, 96.
    - Post-Order: 16, 56, 48, 32, 72, 84, 96, 88, 80, 64.
    - Notice In-Order Traversal sorts in sorted order.

![alt text](https://github.com/eyc94/Notes/blob/master/images/traversal_options.png "Traversal Options For BST")

- Simple recursive implementation for all traversals. Below is for In-Order BST Traversal:

```python
inOrder(N):
    if N is not NULL:
        inOrder(N.left)
        process N
        inOrder(N.right)
```

#### Breadth First Traversal
- One main breadth-first traversal called **Level-Order Traversal**.
- Processes a tree level by level.
- Level-Order Traversal: 64, 32, 80, 16, 48, 72, 88, 56, 84, 96.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bfs_traversal.png "Example of Breadth-First Search on BST")

- Level-Order Traversal uses a queue:

```java
public static void levelOrder(Node root) {

    Queue<Node> bfsQueue = new ArrayList<>();
    bfsQueue.add(root);

    while (!bfsQueue.isEmpty()) {
        Node currentNode = bfsQueue.remove();
        // Process node.
        System.out.println(currentNode.val);

        if (currentNode.left != null) {
            bfsQueue.add(currentNode.left);
        }
        if (currentNode.right != null) {
            bfsQueue.add(currentNode.right);
        }
    }
}
```