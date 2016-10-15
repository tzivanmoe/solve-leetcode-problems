# Permutations

Given a collection of distinct numbers, return all possible permutations.

For example,

`[1,2,3]` have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

**Solution:**
```java
public class Solution {
  public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
        
    if (nums.length == 0) 
      return res;
        
    res.add(new ArrayList<Integer>(Arrays.asList(nums[0])));
        
    for (int i = 1; i< nums.length; i++) {
      List<List<Integer>> next = new ArrayList<>();
            
      for (int j = 0; j <= i; j++) {
        for (List<Integer> list : res) {
          // make a copy of existing perm
          List<Integer> copy = new ArrayList<>(list);
          copy.add(j, nums[i]);
          next.add(copy);
        }
      }
            
      res = next;
    }
        
    return res;
  }
}
```