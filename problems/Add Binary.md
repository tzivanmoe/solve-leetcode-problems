# Add Binary

Given two binary strings, return their sum (also a binary string).

For example,

a = `"11"`

b = `"1"`

Return `"100"`.

**Solution:**
```java
public class Solution {
  public String addBinary(String s1, String s2) {
    int i = s1.length() - 1, j = s2.length() - 1, c = 0;
    String s = "";

    while (i >= 0 || j >= 0 || c == 1) {
      int a = (i < 0) ? 0 : s1.charAt(i--) - '0';
      int b = (j < 0) ? 0 : s2.charAt(j--) - '0';

      s = (char)('0' + a ^ b ^ c) + s;
      c = (a + b + c) >> 1;
    }

    return s;
  }
}
```