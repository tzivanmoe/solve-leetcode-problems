# Alien Dictionary

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

For example,

Given the following words in dictionary,
```
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
```
The correct order is: `"wertf"`.

**Note:**

1. You may assume all letters are in lowercase.
2. If the order is invalid, return an empty string.
3. There may be multiple valid order of letters, return any one of them is fine.

**Solution:**
```java
public class Solution {
  public String alienOrder(String[] words) {
    if (words == null || words.length == 0)
      return null;

    if (words.length == 1) {
      return words[0];
    }

    Map<Character, List<Character>> adjList = new HashMap<Character, List<Character>>();

    for (int i = 0; i < words.length - 1; i++) {
      String w1 = words[i], w2 = words[i + 1];
      int n1 = w1.length(), n2 = w2.length();

      boolean found = false;

      for (int j = 0; j < Math.max(w1.length(), w2.length()); j++) {
        Character c1 = j < n1 ? w1.charAt(j) : null, c2 = j < n2 ? w2.charAt(j) : null;

        if (c1 != null && !adjList.containsKey(c1)) {
          adjList.put(c1, new ArrayList<Character>());
        }

        if (c2 != null && !adjList.containsKey(c2)) {
          adjList.put(c2, new ArrayList<Character>());
        }

        if (c1 != null && c2 != null && c1 != c2 && !found) {
          adjList.get(c1).add(c2);
          found = true;
        }
      }
    }

    Set<Character> visited = new HashSet<>();
    Set<Character> loop = new HashSet<>();
    Stack<Character> stack = new Stack<Character>();

    for (Character key : adjList.keySet()) {
      if (!visited.contains(key)) {
        if (!topologicalSort(adjList, key, visited, loop, stack)) {
          return "";
        }
      }
    }

    StringBuilder sb = new StringBuilder();

    while (!stack.isEmpty()) {
      sb.append(stack.pop());
    }

    return sb.toString();
  }

  boolean topologicalSort(Map<Character, List<Character>> adjList, char u, Set<Character> visited, Set<Character> loop, Stack<Character> stack) {
    visited.add(u);
    loop.add(u);

    if (adjList.containsKey(u)) {
      for (int i = 0; i < adjList.get(u).size(); i++) {
        char v = adjList.get(u).get(i);

        if (loop.contains(v))
          return false;

        if (!visited.contains(v)) {
          if (!topologicalSort(adjList, v, visited, loop, stack)) {
            return false;
          }
        }
      }
    }

    loop.remove(u);

    stack.push(u);
    return true;
  }
}
```