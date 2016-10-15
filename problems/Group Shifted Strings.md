# Group Shifted Strings

Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep "shifting" which forms the sequence:

```
"abc" -> "bcd" -> ... -> "xyz"
```

Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

For example, given: `["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"]`,

A solution is:

```
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
```

**Solution:**
```java
public class Solution {
  public List<List<String>> groupStrings(String[] strings) {
    List<List<String>> res = new ArrayList<>();
    Map<String, List<String>> map = new HashMap<>();

    for (int i = 0; i < strings.length; i++) {
      String s = strings[i];
      String key = hash(s);

      List<String> list = map.containsKey(key) ? map.get(key) : new ArrayList<String>();
      list.add(s);
      map.put(key, list);
    }

    for (List<String> list : map.values()) {
      Collections.sort(list);
      res.add(list);
    }

    return res;
  }

  String hash(String s) {
    String key = "";

    for (int i = 1; i < s.length(); i++) {
      int diff = (int)(s.charAt(i) - s.charAt(i - 1));
      if (diff < 0) diff += 26;
      key += String.valueOf(diff);
    }

    return key;
  }
}
```