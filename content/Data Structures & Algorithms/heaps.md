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

#### Adding


#### Removing