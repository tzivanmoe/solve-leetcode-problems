# Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

**Solution:**
```java
public class Solution {
  public List<String> generateParenthesis(int n) {
    List<String> res = new ArrayList<String>();
    helper(n, 0, 0, "", res);
    return res;
  }
    
  private void helper(int n, int left, int right, String sol, List<String> res) {
    if (right == n) {
      res.add(sol);
      return;
    }
      
    if (left < n) {
      helper(n, left + 1, right, sol + "(", res);
    }
      
    if (right < left) {
      helper(n, left, right + 1, sol + ")", res);
    }
  }
}
```