# Decode Ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,

Given encoded message `"12"`, it could be decoded as `"AB"` (1 2) or `"L"` (12).

The number of ways decoding `"12"` is 2.

**Solution:**
```java
public class Solution {
  public int numDecodings(String s) {
    if (s == null || s.length() == 0)
      return 0;

    if (s.charAt(0) == '0')
      return 0;

    int n = s.length();

    int[] dp = new int[n + 1];

    dp[0] = 1; dp[1] = 1;

    for (int i = 2; i <= n; i++) {
      int count = 0;

      if (s.charAt(i - 1) > '0')
        count = dp[i - 1];

      if (s.charAt(i - 2) == '1' || (s.charAt(i - 2) == '2' && s.charAt(i - 1) <= '6'))
        count += dp[i - 2];

      dp[i] = count;
    }

    return dp[n];
  }
}
```
