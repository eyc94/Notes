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
- If items are labeled 1..n, then a subproblem would be to find an optimal solution for *S<sub>k</sub> = \{items labeled 1, 2,.. k\}}*.