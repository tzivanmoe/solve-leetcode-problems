# Set Matrix Zeroes

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

**Follow up:**

Did you use extra space?

A straight forward solution using O(mn) space is probably a bad idea.

A simple improvement uses O(m + n) space, but still not the best solution.

Could you devise a constant space solution?

**Solution:**
```java
public class Solution {
  public void setZeroes(int[][] matrix) {
    int n = matrix.length;
    int m = matrix[0].length;
        
    // Check if we need to set zeros for first row and column
    boolean cleanFirstRow = false;
    boolean cleanFirstCol = false;
        
    for (int j = 0; j < m; j++) {
      if (matrix[0][j] == 0) {
        cleanFirstRow = true;
        break;
      }
    }
        
    for (int i = 0; i < n; i++) {
      if (matrix[i][0] == 0) {
        cleanFirstCol = true;
        break;
      }
    }
        
    // Use first row and first column to save the flags
    for (int i = 1; i < n; i++) {
      for (int j = 1; j < m; j++) {
        if (matrix[i][j] == 0) {
          matrix[0][j] = 0;
          matrix[i][0] = 0;
        }
      }
    }
        
    // Based on the flags set other cells
    for (int i = 1; i < n; i++) {
      for (int j = 1; j < m; j++) {
        if (matrix[0][j] == 0 || matrix[i][0] == 0) {
          matrix[i][j] = 0;
        }
      }
    }
        
    // At last set the first row and column
    if (cleanFirstRow) {
      for (int j = 0; j < m; j++) {
        matrix[0][j] = 0;
      }
    }
        
    if (cleanFirstCol) {
      for (int i = 0; i < n; i++) {
        matrix[i][0] = 0;
      }
    }
  }
}
```