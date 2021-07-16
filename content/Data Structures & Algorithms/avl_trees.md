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
rotateLeft(N):
    C <- N.right
    N.right <- C.left
    if N.right is not NULL:
        N.right.parent <- N
    C.left <- N
    N.parent <- C
    updateHeight(N)
    updateHeight(C)
    return C
```

- Pseudocode for a right rotation around N:

```
rotateRight(N):
    C <- N.left
    N.left <- C.right
    if N.left is not NULL:
        N.left.parent <- N
    C.right <- N
    N.parent <- C
    updateHeight(N)
    updateHeight(C)
    return C
```

- The two functions return C, which is the new root of the subtree at which the rotation was done.
- We use this retuned C to update N's old parent to point to C.

```
updateHeight(N):
    N.height <- MAX(height(N.left), height(N.right)) + 1
```

- N's new height is now 1 more than the larger of either the heights of the left or right subtrees.
- The function returns node height or -1 if node is null.
- We can incorporate restructuring into the AVL insert and remove operations.

```
avlInsert(tree, key, value):
    insert key, value into tree like normal BST insertion
    N <- newly inserted node
    P <- N.parent
    while P is not NULL:
        rebalance(P)
        P <- P.parent
```

```
avlRemove(tree, key):
    remove key from tree like normal BST removal
    P <- lowest modified node (e.g. parent of removed node)
    while P is not NULL:
        rebalance(P)
        P <- P.parent
```

- The rebalance function:

```
rebalance(N):
    if balanceFactor(N) < -1:
        if balanceFactor(N.left) > 0:
            N.left <- rotateLeft(N.left)
            N.left.parent <- N
        newSubtreeRoot <- rotateRight(N)
        newSubtreeRoot.parent <- N.parent
        N.parent.left or N.parent.right <- newSubtreeRoot
    else if balanceFactor(N) > 1:
        if balanceFactor(N.right) < 0:
            N.right <- rotateRight(N.right)
            N.right.parent <- N
        newSubtreeRoot <- rotateLeft(N)
        newSubtreeRoot.parent <- N.parent
        N.parent.left or N.parent.right <- newSubtreeRoot
    else:
        updateHeight(N)
```

## Time Complexity
- Single Rotation:
    - Constant O(1) time complexity.
    A limited constant number of pointers is updated.
    - The height of two nodes is updated. This is constant time because the update looks at the height of the already recorded child subtree heights.
- At most 2 rotations (double rotation) called during each call to rebalance().
    - rebalance() therefore runs in constant time.
    - rebalance() called once per node while traversing up.
    - At most rebalance() is called h times which is the height of the tree.
    - If tree is balanced, h is log(N).
- Overall complexity of the insert and remove operations of the AVL Tree is *O(log N)*.