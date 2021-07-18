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

## Heap Implementation
- We can use an array (or dynamic array).
- Works with any binary tree, not just heaps.
- Less space efficient if not a complete tree.

#### The Overview
- Root node of heap is at index **0**.
- Left and right children of a node at index **i** are stored in indices **2 * i + 1** and **2 * i + 2**, respectively.
- Parent of a node at index **i** is **(i - 1) / 2** (floor division).
- Example below:

![alt text](https://github.com/eyc94/Notes/blob/master/images/heap_to_array.png "Image of a heap to array conversion")

- Complete trees are easy to implement. If the tree was not complete, it would be difficult like below:

![alt text](https://github.com/eyc94/Notes/blob/master/images/inc_heap_to_array.png "Image of an incomplete heap to array conversion")

- Keep track of the last element and first open spot in the array representation of heap.
    - This is the last element in array and the following empty spot.

![alt text](https://github.com/eyc94/Notes/blob/master/images/last_first_open.png "Image of heap highlighting the last and first open slots")

#### Inserting Into an Array Based Heap
- Follow this:
    1. Put new element at the end of the array.
    2. Find the new element's parent index ((i - 1) / 2)
    3. Compare the value of the inserted element with the value of its parent.
    4. If the value of the parent is greater than new node value, swap the elements in the array and repeat step 2.
        - Do not repeat if element has reached beginning of array.

![alt text](https://github.com/eyc94/Notes/blob/master/images/insert_heap_example.png "Image of a proper heap")

- Let's add node 7 to the heap above:

![alt text](https://github.com/eyc94/Notes/blob/master/images/insert_seven_to_heap.png "Image of inserting node 7 to heap")

- Compute the index of node 7's parent:
    - ((11 - 1) / 2) -> 5.
    - Compare 7 with the value found.
    - 7 is less than 10, so swap.

![alt text](https://github.com/eyc94/Notes/blob/master/images/swap_seven_ten.png "Image of swapping 7 and 10")

- Repeat and compeare 7 to 8 at index ((5 - 1) / 2) -> 2.

![alt text](https://github.com/eyc94/Notes/blob/master/images/swap_seven_eight.png "Image of swapping 7 and 8")

- Finally, compare 7's new parent node 2 at index ((2 - 1) / 2 -> 0).
- We stop now because 2 is less than 7.

#### Removing From an Array Based Heap
- To access the minimum element, return value of first element in the array.
- Removing is more involved:
    1. Remember the value of first element.
    2. Swap first element with the last element. Remove the last element.
    3. If the array is not empty, find the indices of the children of the replacement element
        - **2 * i + 1** and **2 * i + 2**.
        - If both elements fall beyond bounds, stop.
    4. Compare the value of replacement with the minimum value of its two children.
    5. If replacement element's value is less than minimum child's value, swap the two and repeat from step 3.

- Example below shows removing the root node.
- Replace the root (first element) with the last element and remove the last element.

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_step_one.png "Image of step 1 in removing root")

- Percolate the node 32 down the array while comparing it to its minimum value child.
- Swap with the minimum value childs until it reaches its correct place.

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_steps.png "Image of the remaining steps in the remove operation")

#### Building a Heap From an Unsorted Array
