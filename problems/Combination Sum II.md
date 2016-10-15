# Combination Sum II

Given a collection of candidate numbers (**C**) and a target number (**T**), find all unique combinations in C where the candidate numbers sums to **T**.

Each number in **C** may only be used **once** in the combination.

**Note:**

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set `[10, 1, 2, 7, 6, 1, 5]` and target `8`, 
A solution set is: 
```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**Solution:**
```java
public class Solution {
  public List<List<Integer>> combinationSum2(int[] candidates, int target) {
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
      if (i > index && candidates[i] == candidates[i - 1]) {
        continue;
      }
            
      sol.add(candidates[i]);
      helper(candidates, target - candidates[i], i + 1, sol, res);
      sol.remove(sol.size() - 1);
    }
  }
}
```