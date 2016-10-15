# Missing Number

Given an array containing n distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

For example,
Given nums = `[0, 1, 3]` return `2`.

**Note:**

Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

**Solution:**
```java
public class Solution {
  public int missingNumber(int[] nums) {
    int sum = 0, n = nums.length;
        
    for (int i = 0; i < n; i++)
      sum += nums[i];
            
    return n * (1 + n) / 2 - sum;
  }
}
```