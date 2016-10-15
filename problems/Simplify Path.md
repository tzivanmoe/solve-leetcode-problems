# Simplify Path

Given an absolute path for a file (Unix-style), simplify it.

For example,

path = `"/home/"``, => `"/home"`

path = `"/a/./b/../../c/"`, => `"/c"`

**Corner Cases:**

* Did you consider the case where path = `"/../"`?
In this case, you should return `"/"`.
* Another corner case is the path might contain multiple slashes `'/'` together, such as `"/home//foo/"`.
In this case, you should ignore redundant slashes and return `"/home/foo"`.

**Solution:**
```java
public class Solution {
  public String simplifyPath(String path) {
    Set<String> set = new HashSet<>(Arrays.asList("", ".", ".."));
    Deque<String> deque = new ArrayDeque<>();

    for (String token : path.split("/")) {
      if (token.equals("..") && !deque.isEmpty()) 
        deque.pollLast();

      if (set.contains(token)) 
        continue;

      deque.addLast(token);
    }

    StringBuilder sb = new StringBuilder();

    while (!deque.isEmpty()) {
      sb.append("/" + deque.pollFirst());
    }

    return sb.length() == 0 ? "/" : sb.toString();
  }
}
```