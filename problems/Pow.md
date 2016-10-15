# Pow

Implement pow(x, n).

**Solution:**
```java
public class Solution {
  public double myPow(double x, int n) {
    if (x == 0) return 0;
    if (n == 0) return 1;

    double pow = myPow(x, Math.abs(n) / 2);
    double res = pow * pow;

    if ((n & 1) != 0) res *= x;

    return n < 0 ? 1 / res : res;
  }
}
```