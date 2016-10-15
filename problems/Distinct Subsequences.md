# Distinct Subsequences

Given a string S and a string T, count the number of distinct subsequences of T in S.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ACE"` is a subsequence of `"ABCDE"` while `"AEC"` is not).

Here is an example:

S = `"rabbbit"`, T = `"rabbit"`

Return `3`.

**Solution:**
```java
public class Solution {
  public int numDistinct(String s, String t) {
    int n = s.length(), m = t.length();

    // dp(i, j) represents the count of S(1...i) and T(1...j)
    int[][] dp = new int[n + 1][m + 1];

    for (int i = 0; i <= n; i++)
      dp[i][0] = 1;

    for (int i = 1; i <= n; i++) {
      for (int j = 1; j <= m; j++) {
        if (s.charAt(i - 1) == t.charAt(j - 1)) {
          dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
        } else {
          dp[i][j] = dp[i - 1][j];
        }
      }
    }

    return dp[n][m];
  }
}
```