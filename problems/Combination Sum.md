# Combination Sum

Given a set of candidate numbers (**C**) and a target number (**T**), find all unique combinations in **C** where the candidate numbers sums to **T**.

The **same** repeated number may be chosen from **C** unlimited number of times.

**Note:**

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set `[2, 3, 6, 7]` and target `7`, 
A solution set is: 
```
[
  [7],
  [2, 2, 3]
]
```

**Solution:**
```java
public class Solution {
  public List<List<Integer>> combinationSum(int[] candidates, int target) {
    Arrays.sort(candidates);
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    helper(candidates, target, 0, new ArrayList<Integer>(), res);
    return res;
  }
    
  private void helper(int[] candidates, int target, int index, List<Integer> sol, List<List<Integer>> res) {
    if (target == 0) {
      res.add(new ArrayList<Integer>(sol));
      return;
    }
        
    if (target < 0 || index == candidates.length) {
      return;
    }
        
    for (int i = index; i < candidates.length; i++) {
      sol.add(candidates[i]);
      helper(candidates, target - candidates[i], i, sol, res);
      sol.remove(sol.size() - 1);
    }
  }
}
```