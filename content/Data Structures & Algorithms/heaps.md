# Heaps

## Introduction
- Heaps are a special sort of binary tree where a node is larger than the value of its children.
- Quickly insert elements.
- Quickly retrieve the largest element.
- If you pull out elements from a heap one by one, you get a sorted collection.
- There is also the **priority queue** ADT that lets us insert data with an associated priority. However, we can only access item with highest priority.

## Priority Queues and Heaps
- ADT that associates a priority value with each element.
- Highest priority gets dequeued first.
- A **heap** data structure is a complete binary tree in which every node's value is less than or equal to the value of its children.
    - Called **minimizing binary heap** or **min heap**.
    - Can also have a **max heap**.

## Heaps and Priority Queue Basics
- Priority Queue ADT has an interface:
    - **insert()**: Insert an element with a specified priority value.
    - **first()**: Return the element with the lowest priority value (the "first" element in the priority queue).
    - **remove_first()**: Remove (and return) the element with the lowest priority value.

![alt text](https://github.com/eyc94/Notes/blob/master/images/priority_queue_example.png "Image of priority queue as the user sees it")

- Implemented with a data structure called a **heap**.
- Example of min heap with only priority values:

![alt text](https://github.com/eyc94/Notes/blob/master/images/min_heap_example.png "Image of a min heap")

- We keep track of the last filled position and the next open open.

## Heap Operations
- A min (or max) heap is maintained through the addition and removal of nodes by percolation.
- This moves nodes up and down based on their priority value.

#### Adding
- When adding we place new node into next open spot.
- Percolate up until the value is less than (or greater than, for a max heap) both of its children.
- Consider adding node with value 7 to the min heap above.
- First place in next open spot:

![alt text](https://github.com/eyc94/Notes/blob/master/images/add_min_heap_one.png "Image of first step in adding to min heap")

- Percolate up the tree with the following method:

```
while new priority value < parent's priority value:
    swap new node with parent
```

- Node 7 swaps with node 10.

![alt text](https://github.com/eyc94/Notes/blob/master/images/add_min_heap_two.png "Image of second step in adding to min heap")

- Node 7 swaps with node 8.

![alt text](https://github.com/eyc94/Notes/blob/master/images/add_min_heap_three.png "Image of third step in adding to min heap")

- After all swaps, the property of a min heap is restored.

#### Removing
- The root node is the lowest priority value (min heap) or highest priority value (max heap).
- The operations **first()** and **remove_first()** access and remove the root node.
- How to replace the root node?
    - Replace it with the last element in the heap.
    - Fix the heap by percolating that node down.

- For example, look at the very original min heap. We want to remove the root node and replace with node 32.

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_min_heap_one.png "Image of first step in removing from min heap")

- Last node is removed after it replaces root:

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_min_heap_two.png "Image of second step in removing from min heap")

- We percolate the node 32 down using this method:

```
while priority > smallest child priority:
    swap with smallest child
```

- Node 32 follows this path depicted:

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_min_heap_three.png "Image of third step in removing from min heap")

- Our resulting heap:

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_min_heap_four.png "Image of fourth step in removing from min heap")