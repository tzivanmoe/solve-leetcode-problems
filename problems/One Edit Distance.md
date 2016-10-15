# One Edit Distance

Given two strings S and T, determine if they are both one edit distance apart.

**Solution:**
```java
public class Solution {
  public boolean isOneEditDistance(String s, String t) {
    if (s == null || t == null)
      return false;

    if (s.length() > t.length())
      return isOneEditDistance(t, s);

    int i = 0;

    while (i < s.length() && i < t.length()) {
      if (s.charAt(i) != t.charAt(i)) {
        return s.substring(i + 1).equals(t.substring(i + 1)) ||
               s.substring(i).equals(t.substring(i + 1));
      }

      i++;
    }

    return t.length() - i == 1;
  }
}
```