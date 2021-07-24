# Subset Sum
- **Subset Sum** problem asks whether any subset of a given array X\[1..n\] of positive integers sums to a given integer *T*.
- This problem has a recurrence. Use this to transform into a DP algorithm.
    - **Subproblems**: Each subproblem is described by an integer *i* such that 1 <= i <= n + 1, and an integer t <= T. However, subproblems with t < 0 are trivial, so it seems rather silly to memoize them.
    - **Data Structure**: We can memoize our recurrence into a two-dimensional array S[1..n + 1, 0..T], where S[i, t] stores the value of SS(i, t).
    - **Evaluation Order**: Each entry S[i, t] depends on at most two other entries, both of the form SS[i + 1, *]. So we can fill the array by considering rows from bottom to top in the outer loop, and considering the elements in each row in arbitrary order in the inner loop.
    - **Space & Time**: The memoization structure uses O(nT) space. If S[i + 1, t] and S[i + 1, t - X\[i\]] are already known, we can compute S[i, t] in constant time, so the algorithm runs in O(nT) time.

```
FAST-SUBSET-SUM(X[1..n], T)
1.  S[n + 1, 0] <- TRUE
2.  for t <- 1 to T
3.      S[n + 1, t] <- FALSE
4.  for i <- n downto 1
5.      S[i, 0] = TRUE
6.      for t <- 1 to X[i] - 1
7.          S[i, t] <- S[i + 1, t]
8.      for t <- X[i] to T
9.          S[i, t] <- S[i + 1, t] OR S[i + 1, t - X[i]]
10. return S[1, T]
```

- Worst-case running time is O(nT).
- If input size is large, the naive is actually better!
- DP is not always better!