# Minimum Window Substring

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,

**S** = `"ADOBECODEBANC"`

**T** = `"ABC"`

Minimum window is `"BANC"`.

**Note:**

If there is no such window in S that covers all characters in T, return the empty string `""`.

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

**Solution:**
```java
public class Solution {
  public String minWindow(String s, String t) {
    // step 1. create a hashmap for t
    char[] chsT = t.toCharArray();
    char[] chsS = s.toCharArray();

    Map<Character, Integer> map = new HashMap<Character, Integer>();

    for (int i = 0; i < chsT.length; i++) {
      char ch = chsT[i];
      int count = map.containsKey(ch) ? map.get(ch) : 0;
      map.put(ch, count + 1);
    }

    // step 2. use two pointers
    int i = 0, j = 0, count = 0;
    String res = "";

    while (j < s.length()) {
      char ch_j = chsS[j];

      if (map.containsKey(ch_j)) {
        // j find a character, update the count and the map
        if (map.get(ch_j) > 0) {
            count++;
        }
        map.put(ch_j, map.get(ch_j) - 1);

        while (count == t.length()) {
          // count the length of current substring
          if (res.equals("") || j - i + 1 < res.length()) {
            res = s.substring(i, j + 1);
          }

          char ch_i = chsS[i];

          if (map.containsKey(ch_i)) {
            // i find a character, update the count
            if (map.get(ch_i) >= 0) {
              count--;
            }
            map.put(ch_i, map.get(ch_i) + 1);
          }

          i++;
        }
      }

      j++;
    }

    return res;
  }
}
```