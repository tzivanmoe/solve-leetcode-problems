# Palindrome Partitioning

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = `"aab"`,

Return
```
[
  ["aa","b"],
  ["a","a","b"]
]
```

**Solution:**
```java
public class Solution {
  public List<List<String>> partition(String s) {
    List<List<String>> res = new ArrayList<List<String>>();
        
    if (s == null || s.length() == 0) {
      return res;
    }
        
    int n = s.length();
        
    // step 1. build the dp matrix to hold the palindrome information
    // dp[i][j] represents whether s[i] to s[j] can form a palindrome
    boolean[][] dp = buildMatrix(s, n);
        
    // step 2. recursively generate the list
    helper(s, dp, 0, n, new ArrayList<String>(), res);
        
    return res;
  }
    
  void helper(String s, boolean[][] dp, int start, int end, List<String> sol, List<List<String>> res) {
    if (start == end) {
      res.add(new ArrayList<String>(sol));
      return;
    }
        
    for (int i = start; i < end; i++) {
      if (dp[start][i]) {
        // s[start] to s[i] is a palindrome
        sol.add(s.substring(start, i + 1));
        helper(s, dp, i + 1, end, sol, res);
        sol.remove(sol.size() - 1);
      }
    }
  }
    
  boolean[][] buildMatrix(String s, int n) {
    boolean[][] dp = new boolean[n][n];
        
    for (int i = n - 1; i >= 0; i--) {
      for (int j = i; j < n; j++) {
        if (s.charAt(i) == s.charAt(j) && (j - i <= 2 || dp[i + 1][j - 1])) {
          dp[i][j] = true;
        }
      }
    }
        
    return dp;
  }
}
```
