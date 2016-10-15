# Rotate Image

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Follow up:**

Could you do this in-place?

Solution:
```java
public class Solution {
  public void rotate(int[][] matrix) {
    if (matrix == null) {
      return;
    }
        
    int n = matrix.length;
    int layers = n / 2;
        
    for (int k = 0; k < layers; k++) {
      for (int i = 0; i < n - 1; i++) {
        int tmp = matrix[k][k + i];
                
        // left to top
        matrix[k][k + i] = matrix[k + n - 1 - i][k];
                
        // bottom to left
        matrix[k + n - 1 - i][k] = matrix[k + n - 1][k + n - 1 - i];
                
        // right to bottom
        matrix[k + n - 1][k + n - 1 - i] = matrix[k + i][k + n - 1];
                
        // top to right
        matrix[k + i][k + n - 1] = tmp;
      }
            
      n -= 2;
    }
  }
}
```