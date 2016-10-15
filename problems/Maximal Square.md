# Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing all 1's and return its area.

For example, given the following matrix:
```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
Return 4.

**Solution:**
```java
public class Solution {
  public int maximalSquare(char[][] a) {
      if (a == null || a.length == 0 || a[0].length == 0)
        return 0;

      int max = 0;
      int n = a.length;
      int m = a[0].length;

      // recurrence formula:
      // dp(i, j) = min{ dp(i-1, j-1), dp(i-1, j), dp(i, j-1) }
      int[][] dp = new int[n + 1][m + 1];

      for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
          if (a[i - 1][j - 1] == '1') {
            dp[i][j] = Math.min(
              dp[i - 1][j - 1], 
              Math.min(dp[i - 1][j], dp[i][j - 1])
            ) + 1;
            max = Math.max(max, dp[i][j]);
          }
        }
      }

      // return the area
      return max * max;
  }
}
```