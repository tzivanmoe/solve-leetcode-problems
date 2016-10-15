# Combinations

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,

If n = 4 and k = 2, a solution is:
```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```
**Solution:**
```java
public class Solution {
  public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> sol = new ArrayList<>();
        
    helper(n, k, 1, sol, res);
        
    return res;
  }
    
  void helper(int n, int k, int m, List<Integer> sol, List<List<Integer>> res) {
    if (sol.size() == k) {
      res.add(new ArrayList<Integer>(sol));
      return;
    }
        
    for (int i = m; i <= n; i++) {
      sol.add(i);
      helper(n, k, i + 1, sol, res);
      sol.remove(sol.size() - 1);
    }
  }
}
```