# House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

**Solution:**
```java
public class Solution {
  public int rob(int[] a) {
    if (a == null || a.length == 0)
      return 0;

    int n = a.length;

    // dp(i) represents the max money by robbing till i-th house
    int[] dp = new int[n + 1];

    dp[1] = a[0];

    for (int i = 2; i <= n; i++) {
      dp[i] = Math.max(dp[i - 1], a[i - 1] + dp[i - 2]);
    }

    return dp[n];
  }
}
```