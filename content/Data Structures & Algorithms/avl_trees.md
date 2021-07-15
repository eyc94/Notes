# AVL Trees

## Introduction
- Binary Search Trees can be unbalanced.
- To be balance, we refer to trees in which all nodes have depth around *log(n)* or less.
- One side can have way more nodes than the other side.
- AVL trees is one solution. This is done by rotating nodes.
- Shorten one side and lengthen the other. This makes the tree more even.
- We explore a type of  self-balancing binary search tree called **AVL Trees**.

## Balance
- A BST is height balanced if, at every node in the tree, the subtree heights of the node's left and right subtrees differ by at most 1.
- Operations in a height-balanced BST are guaranteed to have *O(log(n))* runtime complexity.
- We can use a node's balance factor.

```
balanceFactor(N) = height(N.right) - height(N.left)
```

- Height of null node is -1.
- An entire BST is height balanced if every node in the tree has a balance factor of -1, 0, or 1.
- Negative balance factor is **left-heavy**. This means the left subtree has greater height.
- Positive balance factor is **right-heavy**. This means the right subtree has greater height.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst_balance_factor.png "Images of balanced BSTs")

- All nodes above have a balance factor of -1, 0, or 1 which indicates height balanced tree.
- Below are unbalanced trees.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst_unbalanced.png "Images of unbalanced BSTs")