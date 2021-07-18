# Hash Maps
- Arrays have easy access if we know what index to look for.
- However, if we are looking for something, it can be difficult to find out exactly what element in the array contains that value.
- Our solution is **Hash Maps**.
- We run values through formulas that converts what we are storing into a number.
- Take the modulo of that number based on the size of our array.
- This is therefore the index into our array.
- Can have duplicate indices.
- If done right, we can read/write in constant time.

## Introduction
- Insertion and lookup (sometimes removal) is done efficiently by the map data type.
- Known also as *dictionary* or an *associative array*.

## Maps
- Assume that username or email address is key and value is all other data like phone number, addresses, etc.

![alt text](https://github.com/eyc94/Notes/blob/master/images/map_example_one.png "Image of a map tying keys to more complex data values")

- We can keep track of unique words. The key is the word and the value is the number of occurrences.
- Data Structure:
    - Simple array storing key/value structs.
        - This gives us O(N) insertions and lookups.
        - Or, O(log N) lookups if we ordered the array by key.
    - Can use AVL tree.
        - This gives us O(log N) insertions and lookups.
- We can do better than this by using a hash table.

## Hash Tables
- Like an array but a bit different.
    - Can be indexed by values other than integers.
    - More than 1 element may share an index.
- Use a hash function.
    - Takes a value and maps them to an integer index value.

![alt text](https://github.com/eyc94/Notes/blob/master/images/hash_table_example.png "Image of hash table")

- Hash function computes index in 2 steps:

```
hash = hash_function(key)
index = hash % array_size
```

- Good hash function properties:
    - **Determinism**: Given input should always map to the same hash value.
    - **Uniformity**: Inputs should be mapped as evenly as possible over the output range. Non-uniform function results in many collisions.
    - **Speed**: Low computational burden.

- If we were hashing strings, a simple hash function might sum the ASCII values of the characters:

```
"eat" => 'e' + 'a' + 't' = 101 + 97 + 116 = 314
```

- This can have problems though:

```
"eat" => 'e' + 'a' + 't' = 101 + 97 + 116 = 314
"ate" => 'a' + 't' + 'e' = 97 + 116 + 101 = 314
"tea" => 't' + 'e' + 'a' = 116 + 101 + 97 = 314
```

- For these problems, we can use a shifting operation:

```
"eat" => 'e' + 'a' + 't' = 1 * 101 + 2 * 97 + 4 * 116 = 314
"ate" => 'a' + 't' + 'e' = 1 * 97 + 2 * 116 + 4 * 101 = 314
"tea" => 't' + 'e' + 'a' = 1 * 116 + 2 * 101 + 4 * 97 = 314
```

## Perfect and Minimally Perfect Hash Functions
- **Perfect Hash** function is one that results in no collisions.
- **Minimally Perfect** hash function is one that results in no collisions for a table size that exactly equals the number of elements.
- Minimally perfect hash functions rarely exist.
- We have to look at resolving hash conflicts.