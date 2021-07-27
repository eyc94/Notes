# Knapsack

- Given a set of items, each with a weight and a benefit (value), pack a knapsack with a subset of items to achieve the maximum total benefit (value).
- Total weight that can be carried in the knapsack is no more than some fixed number *W*.
- There are 2 version:
    1. "0-1 Knapsack Problem". Use **Dynamic Programming**. Items are indivisible: you either take an item or not.
        - Extra room in knapsack.
    2. "Fractional Knapsack Problem". Use **Greedy Method**. Items are divisible: You can take any fraction of an item.
        - "Always" fill knapsack.
    3. Bin Packing: Only one bin.
