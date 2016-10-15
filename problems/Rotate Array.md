# Rotate Array

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array `[1,2,3,4,5,6,7]` is rotated to `[5,6,7,1,2,3,4]`.

**Note:**

Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

**Hint:**

Could you do it in-place with O(1) extra space?
Related problem: Reverse Words in a String II

**Solution:**
```java
public class Solution {
  public void rotate(int[] nums, int k) {
    int n = nums.length;
        
    k %= n;
        
    reverse(nums, 0, n - k - 1);
    reverse(nums, n - k, n - 1);
    reverse(nums, 0, n - 1);
  }
    
  private void reverse(int[] nums, int i, int j) {
    while (i < j) {
      int val = nums[i];
      nums[i++] = nums[j];
      nums[j--] = val;
    }
  }
}
```