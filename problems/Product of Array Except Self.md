# Product of Array Except Self

Given an array of *n* integers where *n* > 1, `nums`, return an array output such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

Solve it without division and in O(*n*).

For example, given `[1,2,3,4]`, return `[24,12,8,6]`.

**Follow up:**

Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

**Solution:**
```java
public class Solution {
  public int[] productExceptSelf(int[] nums) {
    int n = nums.length;
        
    int[] left = new int[n];
    left[0] = 1;
        
    for (int i = 1; i < n; i++) {
      left[i] = nums[i - 1] * left[i - 1];
    }
        
    int[] right = new int[n];
    right[n - 1] = 1;
        
    for (int i = n - 2; i >= 0; i--) {
      right[i] = nums[i + 1] * right[i + 1];
    }
        
    int[] res = new int[n];
    for (int i = 0; i < n; i++) {
      res[i] = left[i] * right[i];
    }
        
    return res;
  }
}
```