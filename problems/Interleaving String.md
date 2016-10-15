# Interleaving String

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

For example,

Given:

s1 = `"aabcc"`,
s2 = `"dbbca"`,

When s3 = `"aadbbcbcac"`, return `true`.

When s3 = `"aadbbbaccc"`, return `false`.

**Solution:**
```java
public class Solution {
  public boolean isInterleave(String s1, String s2, String s3) {
    int n1 = s1.length(), n2 = s2.length(), n3 = s3.length();

    if (n1 + n2 != n3)
      return false;

    boolean[][] dp = new boolean[n1 + 1][n2 + 1];

    dp[0][0] = true;

    // first row
    for (int j = 1; j <= n2; j++) {
      dp[0][j] = (s2.charAt(j - 1) == s3.charAt(j - 1)) && dp[0][j - 1];
    }

    // first col
    for (int i = 1; i <= n1; i++) {
      dp[i][0] = (s1.charAt(i - 1) == s3.charAt(i - 1)) && dp[i - 1][0];
    }

    // others
    for (int i = 1; i <= n1; i++) {
      for (int j = 1; j <= n2; j++) {
        dp[i][j] = ((s1.charAt(i - 1) == s3.charAt(i + j - 1)) && dp[i - 1][j]) || 
                   ((s2.charAt(j - 1) == s3.charAt(i + j - 1)) && dp[i][j - 1]);
      }
    }

    return dp[n1][n2];
  }
}
```