# Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,

`[1,1,2]` have the following unique permutations:
```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

**Solution:**
```java
public class Solution {
  public List<List<Integer>> permuteUnique(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    boolean[] used = new boolean[nums.length];
    helper(nums, used, new ArrayList<Integer>(), res);
    return res;
  }
    
  private void helper(int[] nums, boolean[] used, List<Integer> sol, List<List<Integer>> res) {
    if (sol.size() == nums.length) {
      res.add(new ArrayList<Integer>(sol));
      return;
    }
      
    for (int i = 0; i < nums.length; i++) {
      // avoid duplication
      if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
        continue;
      }
        
      if (!used[i]) {
        used[i] = true;
        sol.add(nums[i]);
        helper(nums, used, sol, res);
        sol.remove(sol.size() - 1);
        used[i] = false;
      }
    }
  }
}
```