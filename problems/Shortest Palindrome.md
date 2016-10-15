# Shortest Palindrome

Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

For example:

Given `"aacecaaa"`, return `"aaacecaaa"`.

Given `"abcd"`, return `"dcbabcd"`.

**Solution:**
```java
public class Solution {
  public String shortestPalindrome(String s) {
    String r = new StringBuilder(s).reverse().toString();
    int[] lps = getLPS(s + '|' + r);
    return r.substring(0, r.length() - lps[lps.length - 1]) + s;
  }

  // KMP get longest prefix and suffix count
  int[] getLPS(String s) {
    int[] lps = new int[s.length()];
    int i = 1, len = 0;

    while (i < s.length()) {
      if (s.charAt(i) == s.charAt(len)) lps[i++] = ++len;
      else if (len == 0)                lps[i++] = 0;
      else                              len = lps[len - 1];
    }

    return lps;
  }
}
```