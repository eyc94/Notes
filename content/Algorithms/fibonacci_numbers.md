# Fibonacci Numbers
- The recursive definition of Fibonacci Numbers gives us a recursive algorithm for computing them.

![alt text](https://github.com/eyc94/Notes/blob/master/images/fibo_recursive.png "Image of fibonacci tree using recursion")

```
REC-FIBO(n)
1.  if n = 0
2.      return 0
3.  else if n = 1
4.      return 1
5.  else
6.      return REC-FIBO(n - 1) + REC-FIBO(n - 2)
```

- This is really slow.
- The runtime is exponential in *n*.

## Memoization: Remember Everything
- The recursive algorithm above is horribly slow because we are forced to compute the same fibonacci number over and over and over.
- Speed it up by writing down the results of our recursive calls and looking them up instead of recomputing.
- This technique is called **memoization**.

![alt text](https://github.com/eyc94/Notes/blob/master/images/fibo_memo.png "Image of fibonacci tree using memoization")

```
MEM-FIBO(n)
1.  if n = 0
2.      return 0
3.  else if n = 1
4.      return 1
5.  else
6.      if F[n] is undefined
7.          F[n] <- MEM-FIBO(n - 1) + MEM-FIBO(n - 2)
8.      return F[n]
```

- The array *F* is filled from the bottom up.
- This algorithm performs only O(N) additions.

## Dynamic Programming: Fill Deliberately
- Replaced memoized recurrence with a for-loop that fills the array in order.
- ITER-FIBO below uses O(N) additions and stores O(N) integers.

```
ITER-FIBO(n)
1.  F[0] <- 0
2.  F[1] <- 1
3.  for i <- 2 to n
4.      F[i] <- F[i - 1] + F[i - 2]
5.  return F[n]
```

## Don't Remember Everything After All
- We don't need to keep all data.
- Just keep the newest two elements in the array because each new number relies on the previous two numbers.

```
ITER-FIBO2(n)
1.  prev <- 1
2.  curr <- 0
3.  for i <- 1 to n
4.      next <- curr + prev
5.      prev <- curr
6.      curr <- next
7.  return curr
```