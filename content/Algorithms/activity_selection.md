# Activity-Selection Problem

- Scheduling several competing activities that require exclusive use of a common resource, with a goal of maximum-size set of mutually compatible activities.
- Suppose we have a set *S = {a<sub>1</sub>, a<sub>2</sub>,..., a<sub>n</sub>}* of *n* proposed **activities** that wish to use a resource, such as a lecture hall, which can only serve one activity at a time.
- Each activity *a<sub>i</sub>* has a **start time** *s<sub>i</sub>* and a **finish time** *f<sub>i</sub>*, where 0 ≤ *s<sub>i</sub>* < *f<sub>i</sub>* < ∞.
- Selected activity, *a<sub>i</sub>*, takes place during half-open time interval \[*s<sub>i</sub>*, *f<sub>i</sub>*).
- Activities *a<sub>i</sub>* and *a<sub>j</sub>* are **compatible** if the intervals \[*s<sub>i</sub>*, *f<sub>i</sub>*) and \[*s<sub>j</sub>*, *f<sub>j</sub>*) do not overlap.
- *a<sub>i</sub>* and *a<sub>j</sub>* are compatible if *s<sub>i</sub>* ≥ *f<sub>j</sub>* or *s<sub>j</sub>* ≥ *f<sub>i</sub>*.
    - Basically, one activity has to come and finish before the other to be non-overlapping.
- In this problem, we want to select a maximum-size subset of mutually compatible activities.
- Assume activities are sorted in monotonically increasing order of finish time.
    - *f<sub>1</sub>* ≤ *f<sub>2</sub>* ≤ *f<sub>3</sub>* ≤ ... ≤ *f<sub>n - 1</sub>* ≤ *f<sub>n</sub>*.

Consider the activities below:

![alt text](https://github.com/eyc94/Notes/blob/master/images/activity_selection_table.png "Image of example of activities")

- The subset {*a<sub>3</sub>*, *a<sub>9</sub>*, *a<sub>11</sub>*} consists of mutually compatible activities.
    - This is not a maximum subset.
- The subset {*a<sub>1</sub>*, *a<sub>4</sub>*, *a<sub>8</sub>*, *a<sub>11</sub>*} is a maximum subset.
- So is {*a<sub>2</sub>*, *a<sub>4</sub>*, *a<sub>9</sub>*, *a<sub>11</sub>*}.
- First, start by thinking of a DP solution.
- Then, develop a recursive greedy approach.
- Then, convert recursive algorithm to an iterative one.

## The Optimal Substructure of the Activity-Selection Problem

- *S<sub>ij</sub>* is the set of activities that start after *a<sub>i</sub>* finishes and that finish before *a<sub>j</sub>* starts.
- We want to find a maximum set of mutually compatible activities in *S<sub>ij</sub>*.
    - A maximum set is *A<sub>ij</sub>* that includes activity *a<sub>k</sub>*.
- Including *a<sub>k</sub>* in an optimal solution leaves us with two subproblems.
    - Find mutually compatible activities in the set *S<sub>ik</sub>* (activities that start after *a<sub>i</sub>* finishes and finish before *a<sub>k</sub>* starts).
    - Find mutually compatible activities in the set *S<sub>kj</sub>* (activities that start after *a<sub>k</sub>* finishes and finish before *a<sub>j</sub>* starts).

## Making the Greedy Choice

## A Recursive Greedy Algorithm

```
RECURSIVE-ACTIVITY-SELECTOR(s, f, k, n)
1.  m = k + 1
2.  while m ≤ n and s[m] < f[k]
3.      m = m + 1
4.  if m ≤ n
5.      return {a_m} U RECURSIVE-ACTIVITY-SELECTOR(s, f, m, n)
6.  else return 0
```

- Assuming that the activities are already sorted by increasing finish time, the runtime is &Theta;(N).

## An Iterative Greedy Algorithm

```
GREEDY-ACTIVITY-SELECTOR(s, f)
1.  n = s.length
2.  A = {a_1}
3.  k = 1
4.  for m = 2 to n
5.      if s[m] ≥ f[k]
6.          A = A U {a_m}
7.          k = m
8.  return A
```

- Assume activities are ordered by increasing finish time.
- Runtime is also &Theta;(N) time.