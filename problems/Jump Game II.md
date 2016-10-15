# Jump Game II

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = `[2,3,1,1,4]`

The minimum number of jumps to reach the last index is `2`. (Jump `1` step from index 0 to 1, then `3` steps to the last index.)

**Note:**

You can assume that you can always reach the last index.

**Solution:**
```java
public class Solution {
  public int jump(int[] nums) {
    int reach = 0;
    int last = 0;
    int steps = 0;
        
    for (int i = 0; i < nums.length && i <= reach; i++) {
      if (i > last) {
        steps++;
        last = reach;
      }
            
      if (i + nums[i] > reach) {
        reach = i + nums[i];
      }
    }
        
    if (reach >= nums.length - 1) {
      return steps;
    } else {
      return -1;
    }
  }
}
```
