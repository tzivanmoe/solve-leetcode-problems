# Word Pattern II

Given a `pattern` and a string `str`, find if `str` follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in `pattern` and a non-empty substring in `str`.

**Examples:**

1. pattern = `"abab"`, str = `"redblueredblue"` should return true.
2. pattern = `"aaaa"`, str = `"asdasdasdasd"` should return true.
3. pattern = `"aabb"`, str = `"xyzabcxzyabc"` should return false.

**Notes:**
You may assume both `pattern` and `str` contains only lowercase letters.

Solution:
```java
public class Solution {
  public boolean wordPatternMatch(String pattern, String str) {
    Map<Character, String> map = new HashMap<>();
    Set<String> set = new HashSet<>();

    return isMatch(str, 0, pattern, 0, map, set);
  }

  boolean isMatch(String str, int i, String pat, int j, Map<Character, String> map, Set<String> set) {
    // base case
    if (i == str.length() && j == pat.length()) return true;
    if (i == str.length() || j == pat.length()) return false;

    // get current pattern character
    char c = pat.charAt(j);

    // if the pattern character exists
    if (map.containsKey(c)) {
      String s = map.get(c);

      // then check if we can use it to match str[i...i+s.length()]
      if (!str.startsWith(s, i)) {
        return false;
      }

      // if it can match, great, continue to match the rest
      return isMatch(str, i + s.length(), pat, j + 1, map, set);
    }

    // pattern character does not exist in the map
    for (int k = i; k < str.length(); k++) {
      String p = str.substring(i, k + 1);

      if (set.contains(p)) {
        break;
      }

      // create or update it
      map.put(c, p);
      set.add(p);

      // continue to match the rest
      if (isMatch(str, k + 1, pat, j + 1, map, set)) {
        return true;
      }
    }

    // we've tried our best but still no luck
    // backtracking
    set.remove(map.get(c));
    map.remove(c);

    return false;
  }
}
```