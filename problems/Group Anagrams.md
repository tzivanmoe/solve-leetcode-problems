# Group Anagrams

Given an array of strings, group anagrams together.

For example, given: `["eat", "tea", "tan", "ate", "nat", "bat"]`, 

Return:
```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:** All inputs will be in lower-case.

**Solution:**
```java
public class Solution {
  public List<String> anagrams(String[] strs) {
    List<String> res = new ArrayList<String>();

    if (strs == null) {
        return res;
    }

    Map<String, List<String>> map = new HashMap<String, List<String>>();

    for (int i = 0; i < strs.length; i++) {
      String str = strs[i];
      String key = sort(str);

      List<String> list = map.containsKey(key) ? map.get(key) : new ArrayList<String>();
      list.add(str);

      map.put(key, list);
    }

    for (Map.Entry<String, List<String>> entry : map.entrySet()) {
      String key = entry.getKey();
      List<String> list = entry.getValue();

      if (list.size() > 1) {
        res.addAll(list);
      }
    }

    return res;
  }

  String sort(String str) {
    char[] chars = str.toCharArray();
    Arrays.sort(chars);
    return new String(chars);
  }
}
```