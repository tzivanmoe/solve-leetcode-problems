# House Robber II

Note: This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

**Solution:**
```java
public class Solution {
  public int rob(int[] nums) {
    if (nums == null || nums.length == 0)
      return 0;

    int n = nums.length;

    if (n == 1) 
      return nums[0];

    if (n == 2) 
      return Math.max(nums[0], nums[1]);

    return Math.max(rob(nums, 0, n - 2), rob(nums, 1, n - 1));
  }

  int rob(int[] nums, int s, int e) {
    int n = e - s + 1;

    int[] dp = new int[n + 1];
    dp[1] = nums[s];

    for (int i = 2; i <= n; i++) {
      dp[i] = Math.max(dp[i - 1], nums[s - 1 + i] + dp[i - 2]);
    }

    return dp[n];
  }
}
```