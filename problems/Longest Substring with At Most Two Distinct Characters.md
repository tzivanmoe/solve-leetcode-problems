# Longest Substring with At Most Two Distinct Characters

Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

For example, Given s = `"eceba"`,

T is `"ece"` which its length is 3.

**Solution:**
```java
public class Solution {
  public int lengthOfLongestSubstringTwoDistinct(String s) {
    if (s == null) return 0;

    int i = 0; // slow pointer
    int j = 0; // fast pointer
    int max = 0;

    // use a map to track the char and its count
    Map<Character, Integer> map = new HashMap<Character, Integer>();

    while (j < s.length()) {
      char ch = s.charAt(j);

      if (map.size() < 2 || map.containsKey(ch)) {
        // less than 2 distinct chars or the char is in the map already
        // put it to the map and update the count
        map.put(ch, map.containsKey(ch) ? map.get(ch) + 1: 1);

        // update the max
        max = Math.max(max, j - i + 1);

        j++;
      } else {
        // we keep removing the old chars from the map
        // till we only have one distinct char
        while (map.size() == 2) {
          ch = s.charAt(i);

          map.put(ch, map.get(ch) - 1);

          if (map.get(ch) == 0)
            map.remove(ch);

          i++;
        }
      }
    }

    return max;
  }
}
```