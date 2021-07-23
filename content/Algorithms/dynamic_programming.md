# Dynamic Programming

- Like divide and conquer, DP solves problems by combining the solutions to subproblems.
- Divide and conquer algorithms partition the problem into disjoint subproblems, solve them recursively, and combine their solutions to solve the problem.
- **Dynamic Programming** applies when subproblems overlap. That is, when subproblems share subproblems.
    - Saves the subsubproblems answer in a table to avoid doing work again.
    - Typically applied to **optimization problems**.
    - Can have many solutions.
    - Want the optimal (min or max) value.
- When making dynamic programming algorithm, follow four steps:
    1. Characterize the structure of an optimal solution.
    2. Recursively define the value of an optimal solution.
    3. Compute the value of an optimal solution, typically in a bottom-up fashion.
    4. Construct an optimal solution from computed information.
