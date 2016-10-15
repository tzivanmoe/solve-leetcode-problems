# String to Integer

Implement atoi to convert a string to an integer.

**Hint:** 

Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes:** 

It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**Solution:**
```java
public class Solution {
  public int myAtoi(String str) {
    if (str == null) {
      return 0;
    }

    // trim the leading and trailing spaces
    str = str.trim();

    if (str.length() == 0) {
      return 0;
    }

    char[] chars = str.toCharArray();

    boolean positive = true;

    int i = 0;

    if (chars[0] == '-') {
      positive = false;
      i = 1;
    }

    if (chars[0] == '+') {
      i = 1;
    }

    int num = 0;

    while (i < chars.length) {
      char ch = chars[i++];

      if (ch < '0' || ch > '9') {
        return num;
      }

      int d = (int)(ch - '0');

      if (positive) {
        if (num > (Integer.MAX_VALUE - d) / 10) {
          return Integer.MAX_VALUE;
        }
        num = num * 10 + d;
      } else {
        if (num < (Integer.MIN_VALUE + d) / 10) {
          return Integer.MIN_VALUE;
        }
        num = num * 10 - d;
      }
    }

    return num;
  }
}
```