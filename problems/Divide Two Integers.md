# Divide Two Integers

Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

**Solution:**
```java
public class Solution {
  public int divide(int dividend, int divisor) {
    if (dividend == Integer.MIN_VALUE && divisor == -1) {
      return Integer.MAX_VALUE;
    }

    long p = Math.abs((long)dividend);
    long q = Math.abs((long)divisor);

    int res = 0;

    while (p >= q) {
      int count = 0;
      while (p >= (q << count)) {
        count++;
      }

      p -= q << (count - 1);
      res += 1 << (count - 1);
    }

    return ((dividend^divisor) >>> 31 == 0) ? res : -res;
  }
}
```