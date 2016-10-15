# Subsets

Given a set of distinct integers, nums, return all possible subsets.

**Note:** The solution set must not contain duplicate subsets.

For example,

If nums = `[1,2,3]`, a solution is:
```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

**Solution:**
```java
public class Solution {
  public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    res.add(new ArrayList<Integer>());
        
    Arrays.sort(nums);
        
    for (int i = 0; i < nums.length; i++) {
      int size = res.size();
            
      for (int j = 0; j < size; j++) {
        List<Integer> sol = new ArrayList<Integer>(res.get(j));
        sol.add(nums[i]);
        res.add(sol);
      }
    }
        
    return res;
  }
}
```