# Ugly Number II

Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include `2, 3, 5`. For example, `1, 2, 3, 4, 5, 6, 8, 9, 10, 12` is the sequence of the first `10` ugly numbers.

Note that `1` is typically treated as an ugly number.

**Hint:**

1. The naive approach is to call isUgly for every number until you reach the nth one. Most numbers are not ugly. Try to focus your effort on generating only the ugly ones.
2. An ugly number must be multiplied by either 2, 3, or 5 from a smaller ugly number.
3. The key is how to maintain the order of the ugly numbers. Try a similar approach of merging from three sorted lists: L1, L2, and L3.
4. Assume you have Uk, the kth ugly number. Then Uk+1 must be Min(L1 * 2, L2 * 3, L3 * 5).

**Solution:**
```java
public class Solution {
  public int nthUglyNumber(int n) {
    // 1x2, 2x2, 3x2, 4x2, 5x2 ...
    // 1x3, 2x3, 3x3, 4x3, 5x3 ...
    // 1x5, 2x5, 3x5, 4x5, 5x5 ...

    int[] ugly = new int[n + 1];
    ugly[1] = 1;

    int next2 = 2, next3 = 3, next5 = 5;
    int i2 = 1, i3 = 1, i5 = 1;

    for (int i = 2; i <= n; i++) {
      int min = Math.min(next2, Math.min(next3, next5));

      ugly[i] = min;

      if (min == next2)
        next2 = ugly[++i2] * 2;

      if (min == next3)
        next3 = ugly[++i3] * 3;

      if (min == next5)
        next5 = ugly[++i5] * 5;
    }

    return ugly[n];
  }
}
```