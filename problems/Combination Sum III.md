# Combination Sum III

Find all possible combinations of **k** numbers that add up to a number **n**, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

**Example 1:**

Input: **k** = 3, **n** = 7

Output:
```
[[1,2,4]]
```
**Example 2:**

Input: **k** = 3, **n** = 9

Output:
```
[[1,2,6], [1,3,5], [2,3,4]]
```

Solution:
```java
public class Solution {
  public List<List<Integer>> combinationSum3(int k, int n) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    helper(k, n, 1, new ArrayList<Integer>(), res);
    return res;
  }
    
  private void helper(int k, int n, int index, List<Integer> sol, List<List<Integer>> res) {
    if (n == 0 && k == sol.size()) {
      res.add(new ArrayList<Integer>(sol));
      return;
    }
      
    if (index > 9 || n < 0) {
      return;
    }
      
    for (int i = index; i <= 9; i++) {
      sol.add(i);
      helper(k, n - i, i + 1, sol, res);
      sol.remove(sol.size() - 1);
    }
  }
}
```