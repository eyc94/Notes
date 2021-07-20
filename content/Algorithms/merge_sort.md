# Merge Sort
- Divide and conquer algorithm.
    - **Divide**: Divid the *n*-element sequence to be sorted into two subsequences of *n/2* elements each.
    - **Conquer**: Sort the two subsequences recursively using merge sort.
    - **Combine**: Merge the two sorted subsequences to produce the sorted answer.
- Recursion bottoms out when sequence to be sorted has length 1.
- We need to merge two sorted sequences in the "combine" step. Merge by calling *MERGE(A, p, q, r)* where *A* is an array and *p*, *q*, and *r* are indices into the array.
- MERGE takes time &Theta;(n) where *n = r - p + 1* is the total number of elements being merged.

- Suppose we have two piles of cards face up.
- Each pile is sorted with the smallest on top.
- Merge two piles into a single sorted output pile.
- Compare the top card of both piles and then choose the smaller of the two. Put it face down on the output pile.
- When one input pile becomes empty, just place the remaining of the other input pile into the output pile.
- Each basic step takes constant time.
- Merging takes &Theta;(n) time.

## Pseudocode.
- This implementation utilizes the sentinels and their value, infinity.
- When infinity is encountered, it will always be greater than the other values when it reaches the end.

```
MERGE(A, p, q, r)
1.  n1 = q - p + 1
2.  n2 = r - q
3.  let L[1..n1 + 1] and R[1..n2 + 1] be new arrays
4.  for i = 1 to n1
5.      L[i] = A[p + i - 1]
6.  for j = 1 to n2
7.      R[j] = Q[q + j]
8.  L[n1 + 1] = inf
9.  R[n2 + 1] = inf
10. i = 1
11. j = 1
12. for k = p to r
13.     if L[i] <= R[j]
14.         A[k] = L[i]
15.         i = i + 1
16.     else A[k] = R[j]
17.         j = j + 1
```

![alt text](https://github.com/eyc94/Notes/blob/master/images/mergesort_one.png "Example of steps of mergesort")

![alt text](https://github.com/eyc94/Notes/blob/master/images/mergesort_two.png "Example of steps of mergesort")

- **Loop Invariant**:
    - At the start of each iteration of the **for** loop of lines 12 - 17, the subarray *A\[p..k - 1\]* contains the *k - p* smallest elements of *L\[1..n1 + 1\]* and *R\[1..n2 + 1\]*, in sorted order. Moreover, *L\[i\]* and *R\[j\]* are the smallest elements of their arrays that have not been copied back into *A*.
- MERGE takes &Theta;(n) time.
- MERGE can be a subroutine of MERGE-SORT(A, p, r)

```
MERGE-SORT(A, p, r)
1.  if p < r
2.      q = floor((p + r) / 2)
3.      MERGE-SORT(A, p, q)
4.      MERGE-SORT(A, q + 1, r)
5.      MERGE(A, p, q, r)
```

![alt text](https://github.com/eyc94/Notes/blob/master/images/mergesort_bottom_up.png "Example of steps of mergesort")