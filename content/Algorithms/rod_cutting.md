# Rod Cutting

- The **rod-cutting problem** is the following.
    - Given a rod of length *n* inches and a table of prices *p<sub>i</sub>* for *i* = 1, 2, ..., n, determine the maximum revenue *r<sub>n</sub>* obtainable by cutting up the rod and selling the pieces.

- Consider the case when *n* = 4.
- Figure below shows all the ways to cut up a rod of 4 inches in length, including the way with no cuts at all.

![alt text](https://github.com/eyc94/Notes/blob/master/images/rod_prices.png "Image of rod prices")

![alt text](https://github.com/eyc94/Notes/blob/master/images/rod_cutting_example.png "Image of rod cutting example")

- Can cut a rod of length *n* in 2<sup>n - 1</sup> ways.
- To solve the original problem of size *n*, we solve smaller problems of the same type.
    - After cutting initially, consider two of the pieces as their own independent rod cutting problems.
    - The overall optimal solution uses the optimal solutions to the two related subproblems.
    - Exhibits **optimal substructure**.
- After we cut the initial part, we focus on the remainder (leftover).

## Recursive Top-Down Implementation

```
CUT-ROT(p, n)
1.  if n == 0
2.      return 0
3.  q = -inf
4.  for i = 1 to n
5.      q = max(q, p[i] + CUT-ROD(p, n - i))
6.  return q
```

- The function above:
    - Input is an array *p\[1..n\]* of prices and an integer *n*.
    - Returns the max revenue possible for a rod of length *n*.
    - If *n* = 0, no revenue is possible.
    - Initialize max revenue to negative infinity.
    - For loop correctly computes the max revenue.
    - This program takes a long time to run when taking in large inputs.
- The function above is very **inefficient**.
- This is because the function calls itself recursively over and over again with the same parameter values.
- It solves the same subproblem repeatedly.
- The running time is exponential at *T(N) = 2<sup>N</sup>*
    - This is because the function explores all 2<sup>n - 1</sup> ways of cutting a rod of length *n*.

## Using Dynamic Programming For Optimal Rod Cutting
- Arrange each subproblem to be solved once, saving its solution.
    - If we need this solution again, we can look it up rather than recompute.
- Use additional memory to save computation time.
    - This is called a **time-memory trade-off**.

- Two ways to implement a DP approach.
    1. **Top-Down With Memoization**.
        - Write recursively in a natural manner but save result of subproblems in an array or hash table.
        - Procedure checks if subproblem has been solved before.
        - If it has been, just look it up and retrieve that value rather than recomputing.
        - If not, compute the value in the usual way.
        - It **memoized** or "remembers" what results it has computed before.
    2. **Bottom-Up Method**.
        - Depends on some natural notion of the "size" of a subproblem.
        - Solving subproblems depends on solving smaller subproblems.
        - Sort subproblems by size and solve smallest first.
        - When solving subproblems, we have solved and saved the smaller subproblems, reducing work.
    - Usually both have same running times.

### Code For Top-Down CUT-ROD Procedure With Memoization

```
MEMOIZED-CUT-ROD(p, n)
1.  let r[0..n] be a new array
2.  for i = 0 to n
3.      r[i] = -infinity
4.  return MEMOIZED-CUT-ROD-AUX(p, n, r)
```

```
MEMOIZED-CUT-ROD-AUX(p, n, r)
1.  if r[n] >= 0
2.      return r[n]
3.  if n == 0
4.      q = 0
5.  else q = -infinity
6.      for i = 1 to n
7.          q = max(q, p[i] + MEMOIZED-CUT-ROD-AUX(p, n - i, r))
8.  r[n] = q
9.  return q
```

- The main function MEMOIZED-CUT-ROD initializes a helper array called *r* that has -infinity in all spots.
- Then it calls a helper function, MEMOIZED-CUT-ROD-AUX.
    - This is just a memoized procedure of our CUT-ROD function.
    - First checks to see if value is already known in line 1.
    - If found, returns the value in line 2.
    - If not found, computes the value as usual in lines 3 - 7.
    - Line 8 saves the computed value in the aux array.
    - Line 9 returns the computed value.

### Code For Bottom-Up Method

```
BOTTOM-UP-CUT-ROD(p, n)
1.  let r[0..n] be a new array
2.  r[0] = 0
3.  for j = 1 to n
4.      q = -infinity
5.      for i = 1 to j
6.          q = max(q, p[i] + r[j - i])
7.      r[j] = q
8.  return r[n]
```

- Uses natural ordering of subproblems.
- A subproblem of size *i* is "smaller" than a subproblem of size *j* if *i* < *j*.
    - Line 1 creates a new array to save results of subproblems.
    - Line 2 initializes the first value because rod of length 0 creates no revenue.
    - Lines 3 - 6 solves each subproblem of size *j*.
    - Line 7 saves the value of subproblem.
    - Line 8 returns the value.

- Runtimes of the top-down memoization and bottom-up method are the same at &Theta;(N<sup>2</sup>).