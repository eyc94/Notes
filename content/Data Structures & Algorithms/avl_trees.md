# AVL Trees

## Introduction
- AVL is the initials of the tree's inventors: Adelson-Velsky and Landis.
- Another popular is Red-Black Tree.
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

## AVL Tree Rotations
- We need to make sure the tree always exhibits height balance.
- Check height balance of tree after each insertion and removal of an element and do rebalancing operations known as *rotations* whenever height balance is lost.
- A **rotation** is when one node moves upwards and another moves downwards.
    - Has a center and a direction.
    - We can perform a **left** or a **right** rotation around this center node.
    - Left rotations go counter-clockwise. The center moves downwards to the left. The nodes to its right moves upwards.
    - Right rotations go clockwise. The center moves downwards to the right. The nodes to its left moves upwards.

![alt text](https://github.com/eyc94/Notes/blob/master/images/right_right_imbalance.png "Image of a R-R imbalance")

![alt text](https://github.com/eyc94/Notes/blob/master/images/left_rotation.png "Image of a successful left rotation")

- The node with key 10 is the center.
- The node moves downwards to the left.
- Its right child with key 15 moves upwards.
- This is a **single rotation**.

## Detemining the Rotations Needed
- Rotation (single or double) required when inserting or removing.
- Inserting or removing leaves nodes with balance factors of -2 or 2.
- If N has a balance factor of -2, N is *left-heavy*.
- If N has a balance factor of 2, N is *right-heavy*.
- Refer to the heavier of N's children as C.
- The node C will also have a balance factor of -1, 0, or 1.
- Below are possible scenarios.

![alt text](https://github.com/eyc94/Notes/blob/master/images/left_right_heavy.png "Images of a left-heavy and right-heavy node N")

- If N and C are heavy in the same direction (same sign), a single rotation is needed around N in the opposite direction as N's heaviness.

![alt text](https://github.com/eyc94/Notes/blob/master/images/single_rotation_examples.png "Images of situations where single rotation is needed")

- If N and C are heavy in the opposite directions (opposite signs), a double rotation is needed.
- If N is left-heavy and C is right-heavy, rotate left around C then right around N.
- If N is right-heavy and C is left-heavy, rotate right around C then left around N.

![alt text](https://github.com/eyc94/Notes/blob/master/images/double_rotation_examples.png "Images of situtations where double rotation is needed")

## Rotation Implementations
- Implementation of the rotations in code.

#### Single Rotations
- Single rotation needed to restore height balance at a node N where N's child C is heavy in the same direction as N.
    - Left-left imbalance: N is left-heavy and N's left child C is also left-heavy.
    - Right-right imbalance: N is right-heavy and N's right child C is also right-heavy.
- Can be a left or right rotation.
- Rotation is opposite direction of the imbalance.
    - To fix left-left imbalance at N, we do one right rotation around N.
    - To fix right-riht imbalance at N, we do one left rotation around N.
- We examine a single right rotation. Left rotation is just mirrored.
    - N's balance factor is -2 and the balance factor of N's left child C is -1 or 0.
    - This occurs after insertion into C's left subtree causing it to grow in height by 1.
    - This occurs after removal from N's right subtree causing it to shrink in height by 1.
    - Depicted below:

![alt text](https://github.com/eyc94/Notes/blob/master/images/single_right_rotation.png "Image of a single right rotation example")

- In a right rotation around N, the following will happen:
    - N will become the right child of its current left child C.
    - C's current right child will become N's left child.
    - If N has a parent PN, then C will replace N as PN's child. Otherwise, if N was the root of the entire tree, C will replace N as the root.
- After the right rotation:

![alt text](https://github.com/eyc94/Notes/blob/master/images/post_right_rotation.png "Image of a post right rotation")
