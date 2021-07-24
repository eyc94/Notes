# Longest Common Subsequence (LCS)

- A subsequence of a given sequence is just the given sequence with zero or more elements left out.
- Given a sequence X = (x<sub>1</sub>, x<sub>2</sub>,...,x<sub>m</sub>), another sequence Z = (z<sub>1</sub>, z<sub>2</sub>,...,z<sub>k</sub>) is a **subsequence** of X if there exists a strictly increasing sequence (i<sub>1</sub>, i<sub>2</sub>,...,i<sub>k</sub>) of indices of X such that for all j = 1, 2,...,k, we have x<sub>i<sub>j</sub></sub> = z<sub>j</sub>.
- Z = (B, C, D, B) is a subsequence of X = (A, B, C, B, D, A, B) with index sequence o (2, 3, 5, 7).
- Given two sequences X and Y, we say that sequence Z is a **common sub-sequence** of X and Y if Z is a subsequence of both X and Y.
    - If X = (A, B, C, B, D, A, B) and Y = (B, D, C, A, B, A), the sequence (B, C, A) is a common subsequence of both X and Y.
    - (B, C, A) is not a longest common subsequence however since there is one that's much longer.
    - The sequence (B, C, B, A) is an LCS of X and Y.
    - Same for (B, D, A, B).

- In the **longest-common-subsequence problem**, we are given two sequences X = (x<sub>1</sub>, x<sub>2</sub>,...,x<sub>m</sub>) and Y = (y<sub>1</sub>, y<sub>2</sub>,...,y<sub>n</sub>) and wish to find a maximum-length common subsequence of X and Y.

## Step 1: Characterizing A Longest Common Subsequence
- Brute force is to find all subsequences of X and check each subsequence to see whether it is also a subsequence of Y, keeping track of the longest subsequence we find.
- This approach requires exponential time
- The LCS problem has an optimal-substructure property.
- If X = (A, B, C, B, D, A, B), then X<sub>4</sub> = (A, B, C, B)
- X<sub>0</sub> is the empty sequence.
- An LCS of two sequences contains within it an LCS of prefixes of the two sequences. Thus, the LCS problem has an optimal substructure property.

#### Theorem 15.1 (Optimal Substructure of an LCS)
- Let X = (x<sub>1</sub>, x<sub>2</sub>,...,x<sub>m</sub>) and Y = (y<sub>1</sub>, y<sub>2</sub>,...,y<sub>n</sub>) be sequences, and let Z = (z<sub>1</sub>, z<sub>2</sub>,...,z<sub>k</sub>) be any LCS of X and Y.
    1. If x<sub>m</sub> = y<sub>n</sub>, then z<sub>k</sub> = x<sub>m</sub> = y<sub>n</sub> and Z<sub>k - 1</sub> is an LCS of X<sub>m - 1</sub> and Y<sub>n - 1</sub>.
    2. If x<sub>m</sub> != y<sub>n</sub>, then z<sub>k</sub> != x<sub>m</sub> implies that Z is an LCS of X<sub>m - 1</sub> and Y.
    3. If x<sub>m</sub> != y<sub>n</sub>, then z<sub>k</sub> != y<sub>n</sub> implies that Z is an LCS of X and Y<sub>n - 1</sub>.

## Step 2: A Recursive Solution
- SEE LATER.

## Step 3: Computing the length of an LCS
- We could write an exponential-time recursive algorithm to compute the length of an LCS of two sequences.
- Since LCS problem has only &Theta;(MN) distinct subproblems, we use DP to compute the solutions bottom up.
- Code LCS-LENGTH takes two sequences X = (x<sub>1</sub>, x<sub>2</sub>,...,x<sub>m</sub>) and Y = (y<sub>1</sub>, y<sub>2</sub>,...,y<sub>n</sub>) as inputs.
- Stores the *c\[i, j\]* values in a table *c\[0..m, 0..n\]*, and it computes the entries in **row-major** order.
    - **row-major** means that the procedure fills in the first row of *c* from left to right, then the second row, and so on.
- Maintains a table *b\[1..m, 1..n\]* to help us construct an optimal solution.
- Intuitively, *b\[i, j\]* points to the table entry corresponding to the optimal subproblem solution chosen when computing *c\[i, j\]*
- Procedure returns the *b* and *c* tables.
- *c\[m, n\]* contains the length of an LCS of *X* and *Y*.

```
LCS-LENGTH(X, Y)
1.  m = X.length
2.  n = Y.length
3.  let b[1..m, 1..n] and c[0..m, 0..n] be new tables
4.  for i = 1 to m
5.      c[i, 0] = 0
6.  for j = 0 to n
7.      c[0, j] = 0
8.  for i = 1 to m
9.      for j = 1 to n
10.         if xi == yi
11.             c[i, j] = c[i - 1, j - 1] + 1
12.             b[i, j] = "top_left_arrow"
13.         elseif c[i - 1, j] >= c[i, j - 1]
14.             c[i, j] = c[i - 1, j]
15.             b[i, j] = "top_arrow"
16.         else c[i, j] = c[i, j - 1]
17.             b[i, j] = "left_arrow"
18. return c and b
```

- Table below is what's produced by function above.
- Running time of procedure is &Theta;(MN) since each table entry takes &Theta;(1) time to compute.

![alt text](https://github.com/eyc94/Notes/blob/master/images/lcs_table.png "Image of table to solve LCS")

- This is the *c* and *b* tables computed by LCS-LENGTH on the sequences X = (A, B, C, B, D, A, B) and Y = (B, D, C, A, B, A).
- The square in row *i* and column *j* contains the value of *c\[i, j\]* and the arrow for the value of *b\[i, j\]*.
- The value of 4 in *c\[7, 6\]* in the lower right corner is the length of an LCS (B, C, B, A) of *X* and *Y*.
- *c\[i, j\]* depends on whether x<sub>i</sub> = y<sub>j</sub> and the values in entries *c\[i - 1, j\]*, *c\[i, j - 1\]*, and *c\[i - 1, j - 1\]*, which are computed before *c\[i, j\]*.
- Follow arrows of *b\[i, j\]* starting from lower right corner to reconstruct path.
    - Each "top-left_arrow" corresponds to an entry for which x<sub>i</sub> = y<sub>j</sub> is a member of an LCS.

## Step 4: Constructing an LCS
