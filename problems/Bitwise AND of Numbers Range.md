# Bitwise AND of Numbers Range

Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

For example, given the range [5, 7], you should return 4.

**Solution:**
```java
public class Solution {
  public int rangeBitwiseAnd(int m, int n) {
    return rangeBitwiseAnd(m, n, 0x80000000);
  }

  int rangeBitwiseAnd(int m, int n, int shift) {
    // edge case
    if (m == 0) return 0;

    // find highest bit of m
    while ((shift & m) == 0) {
      if ((shift & n) != 0) return 0;
      shift >>>= 1;
    }

    return shift + rangeBitwiseAnd(m - shift, n - shift, shift);
  }
}
```