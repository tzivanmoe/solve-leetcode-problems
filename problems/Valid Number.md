# Valid Number

Validate if a given string is numeric.

Some examples:

`"0"` => `true`

`" 0.1 "` => `true`

`"abc"` => `false`

`"1 a"` => `false`

`"2e10"` => `true`

**Note:**

It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

**Solution:**
```java
public class Solution {
  public boolean isNumber(String s) {
    if (s == null) return false;

    s = s.trim();
    int n = s.length();

    if (n == 0) return false;

    // Define flags
    int signCount = 0;

    boolean hasE = false;
    boolean hasNum = false;
    boolean hasPoint = false;

    // Go through the characters
    for (int i = 0; i < n; i++) {
      char c = s.charAt(i);

      // invalid character
      if (!isValid(c)) return false;

      // digit
      if (c >= '0' && c <= '9') hasNum = true;

      // e or E
      if (c == 'e' || c == 'E') {
        // e 之前一定要有数字
        if (hasE || !hasNum) return false;
        // e 不能作为最后一个
        if (i == n - 1) return false;

        hasE = true;
      }

      // decimal place
      if (c == '.') {
        // 小数点不能出现在 e 之后
        if (hasPoint || hasE) return false;
        // 小数点如果在最后一位出现，那么前面必须有要数字
        if (i == n - 1 && !hasNum) return false;

        hasPoint = true;
      }

      // signs
      if (c == '+' || c == '-') {
        // 不允许超过两个符号出现
        if (signCount == 2) return false;
        // 不允许符号在最后出现
        if (i == n - 1) return false;
        // 符号出现在中间的前提是前面有 e
        if (i > 0 && !hasE) return false;

        signCount++;
      }
    }

    return true;
  }

  boolean isValid(char c) {
    return c == '.' || c == '+' || c == '-' || c == 'e' || c == 'E' || c >= '0' && c <= '9';
  }
}
```