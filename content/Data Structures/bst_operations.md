# Binary Search Tree Operations

## Introduction
- Finding an element.
- Inserting an element.
- Removing an element.

## Finding an Element in a BST
- We need to provide a key to find in our BST.
- Search the tree much like you would during a binary search on a sorted array.
- High-Level Overview (Find *k<sub>q</sub>*):
    - Pointer to current node. Start at root.
    - If current is None, the key *k<sub>q</sub>* does not exist. Halt search.
    - If current is equal to *k<sub>q</sub>*, search succeeded. Halt search.
    - If *k<sub>q</sub>* is less than current node's key, move current to point to its left child. Repeat.
    - If *k<sub>q</sub>* is greater than the current node's key, move current to point to its right child. Repeat.

```java
public static boolean find(Node root, int key) {
    Node currentNode = root;
    while (currentNode != null) {
        if (currentNode.val == key) {
            return true;
        } else if (currentNode.val < key) {
            currentNode = currentNode.right;
        } else {
            currentNode = currentNode.left;
        }
    }
    return false;
}
```

- The picture below shows the search for the key of 17 in the BST.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst_find.png "Image of find operation in BST")

## Inserting a New Element Into a BST
- Insert new elements as leaves.
- Insert like we are searching in the tree.
- When inserting a new element, instead of stopping if/when a certain key is found, insertion proceeds until reaching a null node.
    - The location of this null node is the location at which to insert the new node.
    - The new node is the child of the null node's parent.

```java
public static void insert(Node root, int key) {
    Node parent = null;
    Node current = root;
    while (current != null) {
        parent = current;
        if (key < current.val) {
            current = current.left;
        } else {
            current = current.right;
        }
    }
    // If the parent is null, indication of empty BST.
    if (parent == null) {
        root = new Node(key);
    // Add the new node to left or right depending on key being < or >= parent's value.
    } else if (parent.val > key) {
        parent.left = new Node(key);
    } else if (parent.val <= key) {
        parent.right = new Node(key);
    }
}
```

- The picture below shows the insertion of a node with a key of 40 in the BST.

![alt text](https://github.com/eyc94/Notes/blob/master/images/bst_insert.png "Image of insert operation in BST")

## Removing an Element From a BST
- Removing a leaf node is easier than removing a root.
- Removing process depends on the node's number of children.
    - No Children: This is a leaf node. Just free that node by pointing its parent node's child to null.
    - One Child: Free that node and move its child to become the new child of the removed node's parent.
    - Two Children: Find the in-order successor.
        - Imagine all elements stored in the tree lined up in ascending order by key.
        - The in-order successor for a node with key *k* is the node corresponding to the very next key after *k* in the sorted elements above.
        - A node N's in-order successor is always the leftmost node in N's right subtree.
        - High-Level description:
            - Denote N's parent as PN. (If N is root, PN is root pointer for the entire tree).
            - Find N's in-order successor S. Denote S's parent as PS.
            - Update pointers to give N's children to S and remove N from the tree.
                - N's left child becomes S's left child.
                - S's right child (may be null) becomes PS's left child.
                - N's right child becomes S's right child.
                - Update PN to replace N with S.
                - Overall, S becomes PN's left or right child or the root of the tree if N was the root.
            - Free N.

```
remove(bst, k):
    N, PN <- find the node to be removed and its parent based on key k, as in the find() function

    if N has no children:
        update PN to point to None instead of N
    else if N has one child:
        update PN to point to N's child instead of N
    else:
        S, PS <- find N's in-order successor and its parent, as described above
        S.left <- N.left
        if S is not N.right:
            PS.left <- S.right
            S.right <- N.right
        update PN to point to S instead of N
    free N
```

## Runtime Complexity of BST Operations
- The main factor in the computational complexity of all three main BST operations (find, insert, remove) comes from the need to search within the tree.
    - Find operation searches for the key.
    - Insert operation searches for the location to insert new node.
    - Remove searches for the query key and its in-order successor.
- Search begins at root.
- The total amount of work done searching in all three operations is *O(h)* where *h* is the height of the tree.
- The height *h* can vary greatly depending on the order of insertion. It can be *log(n)* or *n*.
- Balancing trees can help limit this to *log(n)*.