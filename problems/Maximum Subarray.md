# Maximum Subarray

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[−2,1,−3,4,−1,2,1,−5,4]`,
the contiguous subarray `[4,−1,2,1]` has the largest sum = `6`.

**More practice:**

If you have figured out the *O(n)* solution, try coding another solution using the divide and conquer approach, which is more subtle.

**Solution:**
```java
public class Solution {
  public int maxSubArray(int[] nums) {
    return maxSubArray(nums, 0, nums.length - 1);
  }
    
  int maxSubArray(int[] nums, int lo, int hi) {
    if (lo == hi) {
      return nums[lo];
    }
            
    int mid = lo + (hi - lo) / 2;
        
    int left = maxSubArray(nums, lo, mid);
    int right = maxSubArray(nums, mid + 1, hi);
    int middle = maxMiddleSum(nums, lo, mid, hi);
        
    return Math.max(middle, Math.max(left, right));
  }
    
  int maxMiddleSum(int[] nums, int lo, int mid, int hi) {
    int sum = 0;
        
    int left = Integer.MIN_VALUE;
    for (int i = mid; i >= lo; i--) {
      sum += nums[i];
      left = Math.max(left, sum);
    }
        
    sum = 0;
        
    int right = Integer.MIN_VALUE;
    for (int i = mid + 1; i <= hi; i++) {
      sum += nums[i];
      right = Math.max(right, sum);
    }
        
    return left + right;
  }
}
```