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
