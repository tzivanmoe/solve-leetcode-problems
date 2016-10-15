# Maximum Product Subarray

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = `6`.

**Solution:**
```java
public class Solution {
  public int maxProduct(int[] nums) {
    int n = nums.length;
        
    int res = nums[0];
    int min = nums[0];
    int max = nums[0];
        
    for (int i = 1; i < n; i++) {
      if (nums[i] > 0) {
        max = Math.max(nums[i], max * nums[i]);
        min = Math.min(nums[i], min * nums[i]);
      } else {
        int tmp = max;
        max = Math.max(nums[i], min * nums[i]);
        min = Math.min(nums[i], tmp * nums[i]);
      }
            
      res = Math.max(res, max);
    }
        
    return res;
  }
}
```