# Edit Distance
- The **edit distance** between two strings is the minimum number of letter insertions, letter deletions, and letter substitutions required to transform one string into the other.
    - EX: The edit distance from FOOD and MONEY is at most four.
- Visualize editing process by aligning the strings one above the other.
- A gap in the first word for each insertion.
- A gap in the second for each deletion.
- Columns with different letters are substitutions.

## Recursive Structure
- First need to formulate the problem recursively.
- Our alignment representation has a optimal substructure property.
- Suppose we have gap representation for the shortest edit sequence for two strings.
- **If we remove the last column, the remaining columns must represent the shortest edit sequence for the remaining prefixes.**
- For any two input strings A\[1..m\] and B\[1..n\], we can formulate the edit distance problem recursively as follows:
    - For any indices *i* and *j*, let **Edit(i, j)** denote the edit distance between prefixes A\[1..i\] and B\[1..j\]. We need to compute Edit(m, n).

## Recurrence
- When *i* and *j* are both positive, there are exactly three possibilities for the last column in the optimal alignment of A\[1..i\] and B\[1..j\].
    - **Insertion**: The last entry in the top row is empty. The edit distance is equal to Edit(i, j - 1) + 1. The +1 is the cost of the final insertion, and the recursive expression gives the minimum cost for the remaining alignment.

    ![alt text](https://github.com/eyc94/Notes/blob/master/images/edit_distance_insertion.png "Image of edit distance insertion")

    - **Deletion**: The last entry in the bottom row is empty. The edit distance is equal to Edit(i - 1, j) + 1. The +1 is the cost of the final deletion, and the recursive expression gives the minimum cost for the remaining alignment.

    ![alt text](https://github.com/eyc94/Notes/blob/master/images/edit_distance_deletion.png "Image of edit distance deletion")

    - **Substitution**: Both rows have characters in the last column. If these two characters are different, the edit distance is Edit(i - 1, j - 1) + 1. If they are equal, the substitution is free, so edit distance is Edit(i - 1, j - 1).

    ![alt text](https://github.com/eyc94/Notes/blob/master/images/edit_distance_sub.png "Image of edit distance substitution")

- The generic case analysis breaks down if *i* = 0 or *j* = 0, but those boundary cases are easy to handle.
    - Transforming an empty string into a string of length *j* requires *j* insertions, so Edit(0, j) = j.
    - Transforming a string of length *i* into the empty string requires *i* deletions, so Edit(i, 0) = i.
- Edit distance between two empty strings is zero.
- Edit distance satisfies the following recurrence:

![alt text](https://github.com/eyc94/Notes/blob/master/images/edit_distance_recurrence.png "Image of edit distance recurrence")