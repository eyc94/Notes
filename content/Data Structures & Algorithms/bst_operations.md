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