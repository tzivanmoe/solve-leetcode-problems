# Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
The return format had been changed to zero-based indices. Please read the above updated description carefully.

**The idea:**

We should be able to find the two numbers by scanning the array once (from left to right). We use a hashmap to store the `value:index` for each number, at `i-th` position, we check if the value of `target - nums[i]` exsists in the hashmap and they have different positions.

Time complexity: `O(n)`<br />
Space complexity: `O(n)`

**Solution - Java:**
```java
public class Solution {
  public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        
    for (int i = 0; i < nums.length; i++) {
      int num1 = nums[i];
      int num2 = target - num1;
            
      if (map.containsKey(num2)) {
        return new int[]{map.get(num2) + 1, i + 1};
      }
            
      if (!map.containsKey(num1)) {
        map.put(num1, i);
      }
    }
        
    return new int[]{-1, -1};
  }
}
```

**Solution - JavaScript:**
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  var i, map = {};
    
  for (i = 0; i < nums.length; i++) {
    var key = target-nums[i];
        
    if (key in map && i != map[key]) {
      return [i, map[key]];
    }
        
    map[nums[i]] = i;
  }
    
  return [-1, -1];
};
```
