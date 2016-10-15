# Minimum Path Sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Solution:**
```java
public class Solution {
  public int minPathSum(int[][] grid) {
    int n = grid.length, m = grid[0].length;
        
    int[][] dp = new int[n][m];
        
    dp[0][0] = grid[0][0];
        
    // first row
    for (int j = 1; j < m; j++)
      dp[0][j] = grid[0][j] + dp[0][j - 1];
            
    // first col
    for (int i = 1; i < n; i++)
      dp[i][0] = grid[i][0] + dp[i - 1][0];
        
    for (int i = 1; i < n; i++) {
      for (int j = 1; j < m; j++) {
        dp[i][j] = grid[i][j] + Math.min(dp[i - 1][j], dp[i][j - 1]);
      }
    }
        
    return dp[n - 1][m - 1];
  }
}
```