# Longest Palindromic Substring

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

**Solution:**
```java
public class Solution {
  public String longestPalindrome(String s) {
    int n = s.length();

    String res = null;

    boolean[][] dp = new boolean[n][n];

    for (int i = n - 1; i >= 0; i--) {
      for (int j = i; j < n; j++) {
        dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i <= 2 || dp[i + 1][j - 1]);

        if (dp[i][j] && (res == null || j - i + 1 > res.length())) {
          res = s.substring(i, j + 1);
        }
      }
    }

    return res;
  }
}
```