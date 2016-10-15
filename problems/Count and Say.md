# Count and Say

The count-and-say sequence is the sequence of integers beginning as follows:

`1, 11, 21, 1211, 111221, ...`

`1` is read off as `"one 1"` or `11`.

`11` is read off as `"two 1s"` or `21`.

`21` is read off as `"one 2, then one 1"` or `1211`.

Given an integer n, generate the nth sequence.

**Note:** The sequence of integers will be represented as a string.

**Solution:**
```java
public class Solution {
  public String countAndSay(int n) {
    String t, s = "1";

    while (n-- > 1) {
      int c = 0;
      t = "";

      for (int i = 0; i <= s.length(); i++) {
        if (i == s.length() || (i > 0 && s.charAt(i) != s.charAt(i - 1))) {
          t += String.valueOf(c) + s.charAt(i - 1); c = 0; // say
        }
        c++; // count
      }

      s = t;
    }

    return s;
  }
}
```