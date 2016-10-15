# Strobogrammatic Number

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

For example, the numbers "69", "88", and "818" are all strobogrammatic.

**Solution:**
```java
public class Solution {
  public boolean isStrobogrammatic(String num) {
    if (num == null)
      return false;

    return helper(num, 0, num.length() - 1);
  }

  boolean helper(String s, int lo, int hi) {
    if (lo > hi)
      return true;

    char c1 = s.charAt(lo);
    char c2 = s.charAt(hi);

    int mul = (c1 - '0') * (c2 - '0');

    if (mul == 1 || mul == 54 || mul == 64 || (mul == 0 && c1 == c2))
      return helper(s, lo + 1, hi - 1);

    return false;
  }
}
```