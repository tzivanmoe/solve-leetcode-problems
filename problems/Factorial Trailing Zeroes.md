# Factorial Trailing Zeroes

Given an integer n, return the number of trailing zeroes in n!.

**Note:** Your solution should be in logarithmic time complexity.

**Solution:**
```java
public class Solution {
  public int trailingZeroes(int n) {
    int res = 0;

    while (n > 0) {
      n /= 5; 
      res += n; 
    }

    return res;
  }
}
```