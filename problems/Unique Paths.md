# Unique Paths

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![](robot_maze.png)

Above is a 3 x 7 grid. How many possible unique paths are there?

**Note:** m and n will be at most 100.

**Solution:**
```java
public class Solution {
  public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
        
    // first row
    for (int j = 0; j < n; j++) {
      dp[0][j] = 1;
    }
        
    // first col
    for (int i = 0; i < m; i++) {
      dp[i][0] = 1;
    }
        
    // others
    for (int i = 1; i < m; i++) {
      for (int j = 1; j < n; j++) {
        dp[i][j] = dp[i-1][j] + dp[i][j-1];
      }
    }
        
    return dp[m-1][n-1];
  }
}
```