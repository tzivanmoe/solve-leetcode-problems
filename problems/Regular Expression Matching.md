# Regular Expression Matching

Implement regular expression matching with support for '.' and '*'.
```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

**Solution:**
```java
public class Solution {
  public boolean isMatch(String s, String p) {
    int n = s.length(), m = p.length();
        
    boolean[][] dp = new boolean[n + 1][m + 1];
        
    // initialize
    dp[0][0] = true;
        
    for (int j = 1; j <= m; j++)
      dp[0][j] = j > 1 && p.charAt(j - 1) == '*' && dp[0][j - 2];
        
    for (int i = 1; i <= n; i++) {
      for (int j = 1; j <= m; j++) {
        if (p.charAt(j - 1) != '*')
          dp[i][j] = dp[i - 1][j - 1] && isMatch(s.charAt(i - 1), p.charAt(j - 1));
        else
          dp[i][j] = dp[i][j - 2] || dp[i - 1][j] && isMatch(s.charAt(i - 1), p.charAt(j - 2));
      }
    }
        
    return dp[n][m];
  }
    
  boolean isMatch(char a, char b) {
    return a == b || b == '.';
  }
}
```