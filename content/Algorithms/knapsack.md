# Knapsack

- Given a set of items, each with a weight and a benefit (value), pack a knapsack with a subset of items to achieve the maximum total benefit (value).
- Total weight that can be carried in the knapsack is no more than some fixed number *W*.
- There are 2 version:
    1. **"0-1 Knapsack Problem"**. Use **Dynamic Programming**. Items are indivisible: you either take an item or not.
        - Extra room in knapsack.
    2. **"Fractional Knapsack Problem"**. Use **Greedy Method**. Items are divisible: You can take any fraction of an item.
        - "Always" fill knapsack.
    3. Bin Packing: Only one bin.

## 0-1 Knapsack Brute Force
- Since there are *n* items, there are 2<sup>n</sup> possible combinations of items.
- We go through all combinations and find the one with the most total value and with total weight less than or equal to *W*.
- Running time is O(2<sup>n</sup>).
- Can we do better? Yes, with DP but we need to identify the subproblems.

## Defining a Subproblem
- If items are labeled 1..n, then a subproblem would be to find an optimal solution for *S<sub>k</sub> = \{items labeled 1, 2,.. k\}*.
- This is a valid subproblem definition.
- The question is: Can we describe the final solution *S<sub>n</sub>* in terms of subproblems *S<sub>k</sub>*?
- Unfortunately, no we cannot. We need another one.
- Add another parameter *w*, which will represent the *exact* weight for each subset of items.
- The subproblem then will be to compute *B\[k, w\]*.

- Below is the recursive formula:
```
B[k, w] = B[k - 1, w]                                               if wk > w

        or

        = max{B[k - 1, w], B[k - 1, w - wk] + bk}                   if wk <= w           
```

- In B\[k, w\], the *k* is the 1st *k* in our set S = \{1,.. k\}.
- *w* is the weight.
- The best subset of *S<sub>k</sub>* that has the total weight *w*, either contains item *k* or not.
    - **First Case**: *w<sub>k</sub>* > *w*. Item *k* cannot be part of the solution, since if it was, the total weight would be > *w*. So, we select the "optimal" using items 1,.. *k* - 1.
    - **Second Case**: *w<sub>k</sub>* <= *w*. Then the item *k* can be in the solution, and we choose the case with the greater value.
        - It means: The best subset of *S<sub>k</sub>* that has total weight *w* is one of the two:
            - **Do not use item k**: The best subset of *S<sub>k-1</sub>* that has total weight *w*.
            - **Use item k**: The best subset of *S<sub>k-1</sub>* that has total weight *w* - *w<sub>k</sub>* plus the item *k* with benefit *b<sub>k</sub>*.

## Pseudocode

```
1.  for w = 0 to W
2.      B[0, w] = 0
3.  for i = 0 to n                                          // Start with 1 item.
4.      B[i, 0] = 0
5.      for w = 0 to W                                      // Grow the weight of knapsack.
6.          if wi <= w                                      // item i can be part of the solution.
7.              if bi + B[i - 1, w - wi] > B[i - 1, w]      // Use it.
8.                  B[i, w] = bi + B[i - 1, w - wi]
9.              else                                        // Don't use it.
10.                 B[i, w] = B[i - 1, w]
11.         else B[i, w]= B[i - 1, w]                       // Doesn't fit.
```

- B\[n, W\] where *n* = all items and *W* = all capacity of knapsack.

## Runtime
- First for loop is *O(W)*.
- Third for loop is *O(W)* and we repeat this 3rd loop *n* times because of our second for loop.
- Runtime is *O(nW)* which is pseudo-polynomial.
- Remember that brute force is *O(n2<sup>n</sup>)*. Better than brute force is *W* << 2<sup>n></sup>.

## Example 1

- Use the data and run the algorithm above:

- n = 4 (# of elements)
- W = 5 (max weight)
- Elements (weight, benefit): S = \{(2, 3), (3, 4), (4, 5), (5, 6)\}.

0|1|2|3|4
-|-|-|-|-
0|0|0|0|0
0|3|3|3|3
0|3|4|4|4
0|3|4|5|5
0|3|7|7|7