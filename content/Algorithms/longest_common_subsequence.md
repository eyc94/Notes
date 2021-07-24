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

## Step 2: A Recursive Solution
