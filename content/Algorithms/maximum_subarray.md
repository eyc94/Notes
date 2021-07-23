# The Maximum-Subarray Problem

- You're given the future stock prices of a company.
- Find the best time to buy and sell stock to maximize profit.

![alt text](https://github.com/eyc94/Notes/blob/master/images/stock_prices.png "Graph of Stock Prices")

## Brute-Force Solution
- The brute force solution is to find every possible pair and choose the one that gives the most profit.

## An Alternative Approach
- Look at daily change in prices.

![alt text](https://github.com/eyc94/Notes/blob/master/images/max_subarray_solution.png "Second array of daily changes")

- This is still &Theta;(N<sup>2</sup>) runtime.
- Keep in mind that the input must have some negatives or it will not work.

## Solution Using Divide & Conquer

![alt text](https://github.com/eyc94/Notes/blob/master/images/divide_and_conquer_solution.png "Solution Using Divide and Conquer")

- We want to find maximum subarray *A\[low..high\]*.
- We divide into two subarrays of equal size by finding *mid*.
- The two subarrays are *A\[low..mid\]* and *A\[mid + 1..high\]*.
- Any contiguous subarray *A\[i..j\]* of *A\[low..high\]* must lie in exactly one of the following:
    - Entirely in the subarray *A\[low..mid\]*, so that *low <= i <= j <= mid*
    - Entirely in the subarray *A\[mid + 1..high\]*, so that *mid < i <= j <= high*.
    - Crossing the midpoint, so that *low <= i <= mid < j <= high*.
- We can find maximum subarrays for the two subarrays recursively.
- Find the maximum subarray crossing the midpoint.
    - We can find the maximum subarray crossing the midpoint in linear time.
    - This is made up of two subarrays *A\[i..mid\]* and *A\[mid + 1..j\]* where *low <= i <= mid* and *mid < j <= high*.
    - Then combine the two subarrays.
- Take the largest of the three as the solution.

- To find the maximum subarray crossing the midpoint:

```
FIND-MAX-CROSSING-SUBARRAY(A, low, mid, high)
1.  left-sum = inf
2.  sum = 0
3.  for i = mid downto low
4.      sum = sum + A[i]
5.      if sum > left-sum
6.          left-sum = sum
7.          max-left = i
8.  right-sum = -inf
9.  sum = 0
10. for j = mid + 1 to high
11.     sum = sum + A[j]
12.     if sum > right-sum
13.         right-sum = sum
14.         max-right = j
15. return (max-left, max-right, left-sum + right-sum)
```

- The solution above returns a tuple containing the indices for the maximum subarray that crosses the midpoint, along with the sum of the values of a max subarray.
- Lines 1 - 7 find a maximum subarray of left half.
- *left-sum* is the greatest sum found so far.
- *sum* is the holds the sum of entries in *A\[i..mid\]*.
- Update the *left-sum* if the current *sum* is greater than the *left-sum*.

- Divide and conquer algorithm:

```
FIND-MAXIMUM-SUBARRAY(A, low, high)
1.  if high == low
2.      return (low, high, A[low])
3.  else mid = floor((low + high) / 2)
4.      (left-low, left-high, left-sum) = FIND-MAXIMUM-SUBARRAY(A, low, mid)
5.      (right-low, right-high, right-sum) = FIND-MAXIMUM-SUBARRAY(A, mid + 1, high)
6.      (cross-low, cross-high, cross-sum) = FIND-MAXIMUM-SUBARRAY(A, low, mid, high)
7.      if left-sum >= right-sum and left-sum >= cross-sum
8.          return (left-low, left-high, left-sum)
9.      elseif right-sum >= left-sum and right-sum >= cross-sum
10.         return (right-low, right-high, right-sum)
11.     else return (cross-low, cross-high, cross-sum)
```

## Analyzing the Divide and Conquer Algorithm
- Assume the input size is a power of 2.
- The base case when *n* = 1 is constant time.
    - *T(1) = &Theta;(1)*.
- Recursive case occurs when *n* > 1.
    - *T(N) = &Theta;(1) + 2T(N/2) + &Theta;(N) + &Theta;(1)*.
    - *T(N) = 2T(N/2) + &Theta;(N)*.
- Same as Merge Sort.
- Recurrence has the solution *T(N) = &Theta;(N lg N)*.