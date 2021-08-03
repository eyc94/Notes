# Huffman Codes
- Compress data very effectively.
- Savings of 20% to 90% are typical.
- Data is a sequence of characters.
- Huffman's greedy algorithm uses a table giving how often each character occurs to build up an optimal way of representing each character as a binary string.

## Constructing A Huffman Code
- Huffman invented a greedy algorithm that constructs an optimal prefix code called a **Huffman Code**.

```
HUFFMAN(C)
1.  n = |C|
2.  Q = C
3.  for i = 1 to n - 1
4.      allocate a new node z
5.      z.left = x = EXTRACT-MIN(Q)
6.      z.right = y = EXTRACT-MIN(Q)
7.      z.freq = x.freq + y.freq
8.      INSERT(Q, z)
9.  return EXTRACT-MIN(Q)       // Return the root of the tree
```