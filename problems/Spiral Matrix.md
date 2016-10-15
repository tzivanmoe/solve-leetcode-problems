# Spiral Matrix

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```
You should return `[1,2,3,6,9,8,7,4,5]`.

**Solution:**
```java
public class Solution {
  public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> res = new ArrayList<Integer>();
        
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
      return res;
    }
        
    int m = matrix.length;
    int n = matrix[0].length;
        
    int layers = (int)Math.ceil(Math.min(m, n) / 2.0);
        
    for (int k = 0; k < layers; k++) {
      if (m <= 0 || n <= 0) {
        break;
      }
            
      // one row
      if (m == 1) {
        for (int j = 0; j < n; j++) {
          res.add(matrix[k][k + j]);
        }
      }
            
      // one column
      else if (n == 1) {
        for (int i = 0; i < m; i++) {
          res.add(matrix[k + i][k]);
        }
      }
            
      else {
        // top
        for (int j = 0; j < n - 1; j++) {
          res.add(matrix[k][k + j]);
        }
                
        // right
        for (int i = 0; i < m - 1; i++) {
          res.add(matrix[k + i][k + n - 1]);
        }
                
        // bottom
        for (int j = n - 1; j > 0; j--) {
          res.add(matrix[k + m - 1][k + j]);
        }
                
        // left
        for (int i = m - 1; i > 0; i--) {
          res.add(matrix[k + i][k]);
        }
      }
            
      m -= 2;
      n -= 2;
    }
        
    return res;
  }
}
```