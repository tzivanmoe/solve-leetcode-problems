# Spiral Matrix II

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

**Solution:**
```java
public class Solution {
  public int[][] generateMatrix(int n) {
    int[][] res = new int[n][n];
        
    int layers = (int)Math.ceil(n / 2.0);
        
    int val = 1;
        
    for (int k = 0; k < layers; k++) {
      if (n == 1) {
        res[k][k] = val++;
        break;
      }
            
      // top
      for (int j = 0; j < n - 1; j++) {
        res[k][k + j] = val++;
      }
            
      // right
      for (int i = 0; i < n - 1; i++) {
        res[k + i][k + n - 1] = val++;
      }
            
      // bottom
      for (int j = n - 1; j > 0; j--) {
        res[k + n - 1][k + j] = val++;
      }
            
      // left
      for (int i = n - 1; i > 0; i--) {
        res[k + i][k] = val++;
      }
            
      n -= 2;
    }
        
    return res;
  }
}
```