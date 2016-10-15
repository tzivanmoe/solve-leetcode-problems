# Word Pattern

Given a `pattern` and a string `str`, find if `str` follows the same `pattern`.

Here follow means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `str`.

**Examples:**

pattern = `"abba"`, str = `"dog cat cat dog"` should return `true`.

pattern = `"abba"`, str = `"dog cat cat fish"` should return `false`.

pattern = `"aaaa"`, str = `"dog cat cat dog"` should return `false`.

pattern = `"abba"`, str = `"dog dog dog dog"` should return `false`.

**Notes:**

You may assume `pattern` contains only lowercase letters, and `str` contains lowercase letters separated by a single space.

**Solution:**
```java
public class Solution {
  public boolean wordPattern(String pattern, String str) {
    String[] words = str.split(" ");

    if (pattern.length() != words.length) {
      return false;
    }

    Set<String> set = new HashSet<>();
    Map<Character, String> map = new HashMap<>();

    for (int i = 0; i < words.length; i++) {
      String s = words[i];
      char p = pattern.charAt(i);

      if (map.containsKey(p) && !map.get(p).equals(s)) {
        return false;
      }

      if (!map.containsKey(p) && set.contains(s)) {
        return false;
      }

      map.put(p, s);
      set.add(s);
    }

    return true;
  }
}
```