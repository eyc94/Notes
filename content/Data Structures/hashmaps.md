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

## Hash Table Collisions
- Accommodate for when two different inputs hash to the same index.
- There are two ways.

#### Collision Resolution With Chaining
- Store a collection of elements at each index in the hash table array.
- Each collection is called a bucket or a chain.
- Linked Lists are a popular choice.

![alt text](https://github.com/eyc94/Notes/blob/master/images/chaining_example.png "Image of an example of collisions in a chained linked lit")

- Accessing value for a key would be like this:
    - Compute the element's bucket using hash function.
    - Search the data structure at that bucket for the element using the key. (Iterate through Linked List).

- Adding or removing an element is similar.
- The **load factor** of a hash table is the average number of elements in each bucket:

```
?? = n / m
```
- **n** is the total number of elements stored in the table.
- **m** is the number of buckets.
- **??** is the load factor.

- In a chained hash table, load factor can be greater than 1.
- As load factor increases, operations on table will slow down.
- We often double the number of buckets when the load factor reaches a certain limit.
    - Can use dynamic array.
    - Resizing ability is based on the load factor.
    - Resizing is done by recomputing the hash function for each element with the new number of buckets.

- Average case complexity of a Linked List based chained hash table:
    - Assume good distribution hash function.
    - Average case for all operations is **O(??)**.
    - If number of buckets is adjusted according to load factor, the number of elements is a constant factor of the number of buckets:

```
?? = n / m = O(m) / m = O(1)
```

- Average case is constant time.
- Worse case is **O(N)** because all elements can be in the same bucket.

#### Collision Resolution With Open Addressing
- Probe for an empty spot.
- Procedure:
    - Use hash function to compute initial index *i* for the element.
    - If hash table at index *i* is empty, insert element there and stop.
    - If not, increment *i* to the next index in the problem sequence (e.g. *i + 1*) and repeat.
- Probing schemes:
    - Linear probing: *i = i + 1*
    - Quadratic probing: *i = i + j2* (j = 1, 2, 3, ...)
    - Double hashing: *i = i + j * h2(key)* (j = 1, 2, 3, ...)
        - h2 is a second, independent hash function

![alt text](https://github.com/eyc94/Notes/blob/master/images/address_example.png "Image of open address example 1")

- Searching is the same.
- Probe until you find it or until there's an empty spot in which case it doesn't exist.
- Reach the end of the array? Wrap around to the beginning.
- If we removed an element, this could disrupt probing.

![alt text](https://github.com/eyc94/Notes/blob/master/images/address_remove_example.png "Image of an example of disruption after removing element")

- To get around this, we put a tombstone value, **__TS__** after removing.
- This does not halt search when encountering an empty spot.

![alt text](https://github.com/eyc94/Notes/blob/master/images/remove_tombstone_example.png "Image of example of tombstone value")

- We can run into the problem of clustering.
- Too many elements are placed next to each other.
- Below represents a clustering probability:

![alt text](https://github.com/eyc94/Notes/blob/master/images/cluster_probability.png "Image of cluster probability")

- Quadratic probing and double hashing can reduce clusters.
- A table's load factor cannot exceed 1.
- Desired to maintain a low load factor.

##### Complexity Analysis of Open Address Hashing
- Assume truly uniform hashing.
- To insert an item into table, the probability that first probe is successful is: **(m - n) / m**.
    - **m** total slots and **n** filled slots. **m - n** open spots.
    - **p** is the probability so **p = (m - n) / m**.
- If first probe fails, the probability of second probe succeeding is **(m - n) / (m - 1)**.
    - There are still **m - n** remaining open slots.
    - We only have a total of **m - 1** slots to look at because we examined one already.
- If first two fail, the probability of third succeeding is **(m - n) / (m - 2)**.
    - There are still **m - n** open slots.
    - We only have a total of **m - 2** slots to look at since we looked at 2 already.
- This keeps going.
- For each probe, the probability of success is at least **p** because **(m - n) / (m - c) >= (m - n) / m = p**.
- Expected number of probes for any operation is **O(1 / (1 - ??))**.
- For small load factors, our operations will be O(1) on average.