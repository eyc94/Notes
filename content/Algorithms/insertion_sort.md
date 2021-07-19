# Insertion Sort
- Input comes in the form of an array with *n* elements.
- Efficient for sorting a small number of elements.
- It's like sorting a hand of playing cards.
    - Start with an empty left hand.
    - Cards are face down on table.
    - Grab one card at a time and place in left hand.
    - If left hand has cards, compare picked up card to cards in left hand from right to left and put the picked up card in proper place.
    - Left hand is always sorted.

![alt text](https://github.com/eyc94/Notes/blob/master/images/insertion_sort_example.png "Example of insertion sort")

## Pseudocode
- Procedure called **INSERTION-SORT**.
- Takes as parameter an array **A\[1..n\]** containing a sequence of length *n* that is to be sorted.
- *n* is denoted by *A.length*.
- Sorted in-place.

```
INSERTION-SORT(A)
1. for j = 2 to A.length
2.     key = A[j]
3.     // Insert A[j] into the sorted sequence A[1..j - 1].
4.    i = j - 1
5.    while i > 0 and A[i] > key
6.        A[i + 1] = A[i]
7.        i = i - 1
8.    A[i + 1] = key
```

## Loop Invariants and the Correctness of Insertion Sort
- Index *j* indicates "current card" being inserted into hand.
- At the beginning of iteration of for loop, A\[1..j - 1\] constitutes the currently sorted hand.
- The remaining A\[j + 1..n\] corresponds to the pile of cards still on the table.
- Elements from A\[1..j - 1\] are the original j - 1 elements but in sorted order.
- **Loop Invariant**:
    - At the start of each iteration of the **for** loop of lines 1 - 8 in the pseudocode above, the subarray A\[1..j - 1\] consists of the elements originally in A\[1..j - 1\], but in sorted order.
- Must show 3 things about loop invariant:
    - **Initialization**: It is true prior to the first iteration of the loop.
    - **Maintenance**: If it is true before an iteration of the loop, it remains true before the next iteration.
    - **Termination**: When the loop terminates, the invariant gives us a useful property that helps show that the algorithm is correct.