# Longest Substring Without Repeating Characters

Given a string, find the length of the **longest substring** without repeating characters.

**Examples:**

Given `"abcabcbb"`, the answer is `"abc"`, which the length is `3`.

Given `"bbbbb"`, the answer is `"b"`, with the length of `1`.

Given `"pwwkew"`, the answer is `"wke"`, with the length of `3`. Note that the answer must be a **substring**, `"pwke"` is a subsequence and not a substring.

**Solution:**
```java
public class Solution {
  public int lengthOfLongestSubstring(String s) {
    int i = 0, j = 0, max = 0;
    Set<Character> set = new HashSet<>();

    while (j < s.length()) {
      if (!set.contains(s.charAt(j))) {
        set.add(s.charAt(j++));
        max = Math.max(max, set.size());
      } else {
        set.remove(s.charAt(i++));
      }
    }

    return max;
  }
}
```