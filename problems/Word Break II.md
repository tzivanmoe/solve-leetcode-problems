# Word Break II

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

For example, given
s = `"catsanddog"`,
dict = `["cat", "cats", "and", "sand", "dog"]`.

A solution is `["cats and dog", "cat sand dog"]`.

**Solution:**
```java
public class Solution {
  public List<String> wordBreak(String s, Set<String> dict) {
    List<String> res = new ArrayList<String>();
        
    if (!canBreak(s, dict)) return res;
        
    helper(s, dict, 0, "", res);
        
    return res;
  }
    
  void helper(String s, Set<String> dict, int start, String sol, List<String> res) {
    if (start == s.length()) {
      res.add(sol);
      return;
    }
        
    for (int i = start; i < s.length(); i++) {
      String sub = s.substring(start, i + 1);
            
      if (dict.contains(sub)) {
        helper(s, dict, i + 1, sol + (sol.length() == 0 ? "" : " ") + sub, res);
      }
    }
  }
    
  boolean canBreak(String s, Set<String> dict) {
    if (s == null || s.length() == 0) return false;
        
    int n = s.length();
        
    // dp[i] represents whether s[0...i] can be formed by dict
    boolean[] dp = new boolean[n];
        
    for (int i = 0; i < n; i++) {
      for (int j = 0; j <= i; j++) {
        String sub = s.substring(j, i + 1);
                
        if (dict.contains(sub) && (j == 0 || dp[j - 1])) {
          dp[i] = true;
          break;
        }
      }
    }
        
    return dp[n - 1];
  }
}
```