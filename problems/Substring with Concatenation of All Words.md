# Substring with Concatenation of All Words

You are given a string, s, and a list of **words**, **words**, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

For example, given:

s: `"barfoothefoobarman"`

words: `["foo", "bar"]`

You should return the indices: `[0,9]`. (order does not matter).

**Solution:**
```java
public class Solution {
  public List<Integer> findSubstring(String s, String[] words) {
    List<Integer> res = new ArrayList<Integer>();

    int m = words.length;
    int n = words[0].length();
    int len = m * n;

    // build the hash map
    Map<String, Integer> map = new HashMap<String, Integer>();
    for (int i = 0; i < words.length; i++) {
      String word = words[i];

      int count = map.containsKey(word) ? map.get(word) + 1 : 1;
      map.put(word, count);
    }

    for (int i = 0; i < s.length() - len + 1; i++) {
      Map<String, Integer> temp = new HashMap<String, Integer>(map);

      for (int j = i; j < i + len; j += n) {
        String str = s.substring(j, j + n);

        if (temp.containsKey(str)) {
          int count = temp.get(str) - 1;

          if (count == 0) {
            temp.remove(str);
          } else {
            temp.put(str, count);
          }
        } else {
          break;
        }
      }

      if (temp.size() == 0) {
        res.add(i);
      }
    }

    return res;
  }
}
```