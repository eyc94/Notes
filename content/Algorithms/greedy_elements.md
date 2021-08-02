# Elements of the Greedy Strategy

- Obtains optimal solution to a problem by making a sequence of choices.
- Makes choice that seems best at the moment.
- Does not always produce optimal solution but sometimes it does.
- Go through the steps to develop a greedy algorithm:
    1. Determine the optimal substructure of the problem.
    2. Develop a recursive solution.
    3. Show that if we make the greedy choice, then only one subproblem remains.
    4. Prove that it is always safe to make the greedy choice.
    5. Develop a recursive algorithm that implements the greedy strategy.
    6. Convert the recursive algorithm to an iterative algorithm.

## Greedy-Choice Property
- First key ingredient is the **greedy-choice property**:
    - We can assemble a globally optimal solution by making locally optimal (greedy) choices.
    - When we are considering which choice to make, we make the choice that looks best in the current problem, without considering results from subproblems.
- In DP, we make a choice at each step. But, the choice depends on the answer to subproblems.
    - Solve them in a bottom-up manner.
- In Greedy, we make any choice that seems best at the moment and solve the subproblem that remains.
    - Solves in a top-down fashion. Reduces each problem instance to a smaller one.

## Greedy Versus Dynamic Programming
- Two variants of knapsack problem.
- The **0-1 Knapsack Problem**: A thief robbing a store finds *n* items. The *i*th item is worth *v<sub>i</sub>* dollars and weights *w<sub>i</sub>* pounds, where *v<sub>i</sub>* and *w<sub>i</sub>* are integers. The thief wants to take as valuable a load as possible, but he can carry at most *W* pounds in his knapsack, for some integer *W*. Which items should he take?
    - Thief must take all of an item or none.
    - Cannot take part of an item (fraction).
- The **Fractional Knapsack Problem**: Setup is the same but the thief can take fractions of items, rather than a binary choice (0-1) for each item.