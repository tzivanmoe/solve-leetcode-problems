# Edit Distance

Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

1. Insert a character

2. Delete a character

3. Replace a character

**Solution:**
```java
public class Solution {
  public int minDistance(String word1, String word2) {
    int n1 = word1.length(), n2 = word2.length();

    int[][] dp = new int[n1 + 1][n2 + 1];

    for (int j = 1; j <= n2; j++) {
      dp[0][j] = j;
    }

    for (int i = 1; i <= n1; i++) {
      dp[i][0] = i;
    }

    for (int i = 1; i <= n1; i++) {
      for (int j = 1; j <= n2; j++) {
        int replace = dp[i - 1][j - 1] + ((word1.charAt(i - 1) == word2.charAt(j - 1)) ? 0 : 1);
        int delete = dp[i - 1][j] + 1;
        int insert = dp[i][j - 1] + 1;
        dp[i][j] = Math.min(replace, Math.min(delete, insert));
      }
    }

    return dp[n1][n2];
  }
}
```