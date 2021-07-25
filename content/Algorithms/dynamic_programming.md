# Dynamic Programming

- Dynamic Programming is a powerful algorithm design technique for solving problems that:
    - Appear to be exponential but have a poly solution with DP.
    - In many cases are optimization problems (min/max)
    - Defined by or formulated as recurrences with overlapping subproblems.
    - Optimal solution to a problem contains optimal solutions to subproblems.
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

## Elements of Dynamic Programming

- When does the method apply?
- Two key ingredients that an optimization problem must have in order for dynamic programming to apply.
    1. Optimal substructure
    2. Overlapping subproblems

### Optimal Substructure
- Exhibits **optimal substructure** if an optimal solution to the problem contains within it optimal solutions to subproblems.
- Build optimal solution to problem from optimal solutions to subproblems.
- Common patterns in discovering optimal substructure:
    1. You show that a solution to the problem consists of making a choice, such as choosing an initial cut in a rod.
    2. Suppose for a given problem, you are given the choice that leads to an optimal solution. Don't concern with how to get this choice. You just assume it has been given to you.
    3. Given the choice, determine which subproblems ensue and how to characterize the resulting space of subproblems.
    4. You show that the solutions to the subproblems used within an optimal solution to the problem must themselves be optimal by using a "cut-and-paste" technique.
- Try to keep the space as simple as possible and use more when necessary.

- Optimal substructure varies across problem domains in two ways:
    1. How many subproblems an optimal solution to the original problem uses.
    2. How many choices we have in determining which subproblem(s) to use in an optimal solution.

- In the rod-cutting, an optimal solution for cutting up a rod of size *n* uses just one subproblem (*n* - *i*).
- But, we must consider *n* choices for *i* in order to determine which one yields an optimal solution.

- The running time of a DP algorithm depends on the product of two factors:
    1. The number of subproblems overall.
    2. How many choices we look at for each subproblem.
- For the rod-cutting, we had &Theta;(N) subproblems overall.
- We had at most *n* choices to examine for each, yielding an &Theta;(N<sup>2</sup>) running time.

- DP often uses optimal substructure in a bottom-up fashion.
    - We first find an optimal solution to subproblems and, having solved the subproblems, we find an optimal solution to the problem.

- Can use DP to solve *Unweighted Shortest Path*.
- Cannot use DP to solve *Unweighted Longest Simple Path*.

### Overlapping Subproblems
- The space of subproblems must be "small" in the sense that a recursive algorithm for the problem solves the same subproblems over and over, rather than always generating new subproblems.
- The total number of distinct subproblems is typically polynomial in the input size.
- When a recursive algorithm revisits the same problem repeatedly, we say that the optimization problem has **overlapping subproblems**.
- Solve each subproblem once and store in a table to look up when needed using constant time lookup.

## Memoization
- Top-down strategy while having efficiency of bottom-up approach.
- Memoize natural, but inefficient, recursive algorithm.
- A memoized recursive algorithm maintains an entry in a table for the solution to each subproblem.
- Look up the value stored in table when we encounter problem again.