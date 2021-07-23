# Quick Sort

- Recursive sorting algorithm.
- The hard work is splitting the array into smaller subarrays *before* recursion, so that merging the sorted subarrays is trivial.
    1. Choose a *pivot* element from the array.
    2. Partition the array into three subarrays containing the elements smaller than the pivot, the pivot element itself, and the elements larger than the pivot.
    3. Recursively quicksort the first and last subarrays.

![alt text](https://github.com/eyc94/Notes/blob/master/images/quick_sort_example.png "Image of quick sort example")

## Pseudocode

```
QUICKSORT(A[1..n]):
    if (n > 1)
        Choose a pivot element A[p]
        r <- PARTITION(A, p)
        QUICKSORT(A[1..r - 1])
        QUICKSORT(A[r + 1..n])
```

```
PARTITION(A[1..n], p):
    swap A[p] <-> A[n]
    l <- 0
    for i <- 1 to n - 1
        if A[i] < A[n]
            l <- l + 1
            swap A[l] <-> A[i]
    swap A[n] <-> A[l + 1]
    return l + 1
```

## Analysis of Quick Sort
- T(N) = *O(N lg N)*.