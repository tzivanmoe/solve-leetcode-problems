# Search a 2D Matrix II

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

For example,

Consider the following matrix:
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Given **target** = `5`, return `true`.

Given **target** = `20`, return `false`.

**Solution:**
```java
public class Solution {
  public boolean searchMatrix(int[][] matrix, int target) {
    int n = matrix.length, m = matrix[0].length;

    int i = 0, j = m - 1;

    while (i < n && j >= 0) {
      if (matrix[i][j] == target)
        return true;

      if (target < matrix[i][j])
        j--;
      else
        i++;
    }

    return false;
  }
}
```