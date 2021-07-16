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

## Double Rotations
- Double rotation is needed to restore height balance at a node N where N's child C is heavy in the opposite direction as N.
    - Left-right imbalance: N is left-heavy and N's left child C is right-heavy.
    - Right-left imbalance: N is right-heavy and N's right child C is left-heavy.
- Consists of two single rotations.
    - First is always centered around N's child C.
    - The second is always centered around N itself.
- Fix a left-right imbalance:
    - Apply a left rotation around C followed by a right rotation around N.
- Fix a right-left imbalance:
    - Apply a right rotation around C followed by a left rotation around N.
- Picture below is fixing a left-right imbalance.

![alt text](https://github.com/eyc94/Notes/blob/master/images/before_rotation.png "Image before first rotation")

![alt text](https://github.com/eyc94/Notes/blob/master/images/first_rotation.png "Image of left rotation")

![alt text](https://github.com/eyc94/Notes/blob/master/images/second_rotation.png "Image of right rotation")

- The first rotation creates a same side imbalance.
- Below is the visuals:

- This is the left-right imbalance:

![alt text](https://github.com/eyc94/Notes/blob/master/images/visual_left_right_imbalance.png "Image of a left right imbalance")

- Perform a left rotation around C:
    - G moves up to replace C as N's left child.
    - C moves down to become G's left child.
    - LG becomes C's right child.

![alt text](https://github.com/eyc94/Notes/blob/master/images/visual_left_rotation.png "Image of a left rotation around C")

- Perform a right rotation around N:
    - G moves up to become new root of this subtree.
    - If N originally had a parent PN, G would replace N as the child of PN after double rotation.
    - If N was the root of the tree, G becomes the new root.

![alt text](https://github.com/eyc94/Notes/blob/master/images/visual_right_rotation.png "Image of a right rotation around N")

## Practical Implementation
- How does the AVL Tree recognize when and where a rotation is needed?
- How does it compute a node's balance factor?
- Let's piece everything together.
    - An AVL Tree will only need to be rebalanced in response to an operation that changes the structure of the tree. (Insertion or Removal).
    - Rebalancing is a bottom-up operation. Rebalancing begins at the location where the structure changed and goes up towards the root.
    - AVL recomputes the balance factor every time and rotates if needed.
- We need to find a way to retrace our path. Do this by using pointers to parent nodes.
- If we were writing a class Node to represent each node, we would need the following properties:
    - **key**: An integer that the nodes are sorted by.
    - **value**: Value held at node.
    - **height**: Integer representing height of node.
    - **left**: Left child node.
    - **right**: Right child node.
    - **parent**: Parent node.
    - We use **null** to indicate a node does not have a parent or child.
    - Root's parent is always null.

- Pseudocode for a left rotation around N:

```
```

- Pseudocode for a right rotation around N:

```
```