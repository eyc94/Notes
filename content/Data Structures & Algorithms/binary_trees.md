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

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst.png "Image of Binary Search Tree")