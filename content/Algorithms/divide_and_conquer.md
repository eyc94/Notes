# Divide & Conquer

- Divide & Conquer (D&C) is a top-down algorithm design technique based on multi-branched recursion.
- A D&C algorithm works by recursively breaking down a problem into two or more sub-problems of the same or related type, until these become simple enough to be solved directly.
- The solutions to the sub-problems are then combined to give a solution to the original problem.

- When subproblems are large enough to solve recursively, we call that the **recursive case**.
- When they become small enough that you cannot recurse, it bottoms out and we call that the **base case**.

## Recurrences
- Goes hand in hand with D&C because it gives a natural way to characterize the running times.
- A **recurrence** is an equation or inequality that describes a function in terms of its value on smaller inputs.
- Recurrences take many forms.
    - Does not have to be evenly divided.
    - Could do something like a 2/3 to 1/3 split.

- Three methods to solve recurrences:
    - **Substitution Method**: Guess a bound and then use mathematical induction to prove guess is correct.
    - **Recursion-Tree Method**: Converts the recurrence into a tree whose nodes represent the costs incurred at various levels of the recursion. We use techniques for bounding summations to solve the recurrence.
    - **Master Method**: Provides bounds for recurrences of the form:
        - *T(n) = aT(n/b) + f(n)*
        - *a >= 1*, *b > 1*, and *f(n)* is a given function.