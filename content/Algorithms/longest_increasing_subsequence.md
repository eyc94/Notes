# Longest Increasing Subsequence
- The **Longest Increasing Subsequence (LIS)** problem is to find the length of the longest subsequence of a given sequence such that all elements of the subsequence are sorted in increasing order.

![alt text](https://github.com/eyc94/Notes/blob/master/images/lis_example.png "Image of longest increasing subsequence")

- Two recursive backtracking algorithms for this problem runs in O(2<sup>N</sup>) in the worst case.
- Both can be sped up using DP.

## First Recurrence: Is This Next?
- Can solve in O(N<sup>2</sup>) time using DP.
- Order in which the memoized recursive algorithm fills this array is not immediately clear.
- Each entry *LISbigger\[i, j\]* is filled in *after* the entries *LISbigger\[i, j + 1\]* and *LISbigger\[j, j + 1\]* in the next column shown in figure below:

![alt text](https://github.com/eyc94/Notes/blob/master/images/list_example_two.png "Image of fibonacci tree using recursion")

- Double arrow is the outer loop and the single arrows are inner loops.
- We fill the table from right to left one column at a time.
- Each entry depends on already available entries.
- Code below runs in O(N<sup>2</sup>) time.
- We can reduce space from O(N<sup>2</sup>) to O(N) if we just keep track of the previous two columns.

```
FAST-LIS(A[1..n])
1.  A[0] <- -infinity
2.  for i <- 0 to n
3.      LISbigger[i, n + 1]  <- 0
4.  for j <- n down to 1
5.      for i <- 0 to j - 1
6.          keep <- 1 + LISbigger[j, j + 1]
7.          skip <- LISTbigger[i, j + 1]
8.          if A[i] >= A[j]
9.              LISbigger[i, j] <- skip
10.         else
11.             LISbigger[i, j] <- max{keep, skip}
12. return LISbigger[0, 1]
```

## Second Recurrence: What's Next?
