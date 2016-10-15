# Subsets II

Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,

If **nums** = `[1,2,2]`, a solution is:
```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
**Solution:**
```java
public class Solution {
  public List<List<Integer>> subsetsWithDup(int[] nums) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    res.add(new ArrayList<Integer>());
        
    Arrays.sort(nums);
        
    int lastSize = 0;
        
    for (int i = 0; i < nums.length; i++) {
      int size = res.size();
      int start = (i == 0 || nums[i] != nums[i - 1]) ? 0 : lastSize;
            
      for (int j = start; j < size; j++) {
        List<Integer> sol = new ArrayList<Integer>(res.get(j));
        sol.add(nums[i]);
        res.add(sol);
      }
            
      lastSize = size;
    }
        
    return res;
  }
}
```