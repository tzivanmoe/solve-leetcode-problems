# Single Number III

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given `nums = [1, 2, 1, 3, 2, 5]`, return `[3, 5]`.

**Note:**

1. The order of the result is not important. So in the above example, [5, 3] is also correct.
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

**Solution:**
```java
public class Solution {
  public int[] singleNumber(int[] nums) {
    int xor = 0, a = 0, b = 0;

    for (int i = 0; i < nums.length; i++)
      xor ^= nums[i];

    // Get its last set bit
    xor &= -xor;
    //xor = xor & ~ (xor - 1);

    for (int i = 0; i < nums.length; i++) {
      if ((xor & nums[i]) != 0)
        a ^= nums[i];
      else
        b ^= nums[i];
    }

    return new int[]{a, b};
  }
}
```