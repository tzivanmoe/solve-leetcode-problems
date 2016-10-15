# Wildcard Matching

Implement wildcard pattern matching with support for `'?'` and `'*'`.
```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

**Solution:**
```java
public class Solution {
  public boolean isMatch(String s, String p) {
    int n = s.length(), m = p.length();
        
    boolean[][] dp = new boolean[n + 1][m + 1];
        
    // initialize
    dp[0][0] = true;
        
    for (int j = 1; j <= m; j++) {
      dp[0][j] = dp[0][j - 1] && p.charAt(j - 1) == '*';
    }
        
    for (int i = 1; i <= n; i++) {
      for (int j = 1; j <= m; j++) {
        if (p.charAt(j - 1) != '*') {
          dp[i][j] = dp[i - 1][j - 1] && (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '?');
        } else {
          dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
        }
      }
    }
        
    return dp[n][m];
  }
}
```