# Valid Parentheses

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

**Solution:**
```java
public class Solution {
  public boolean isValid(String s) {
    char[] p = "(){}[]".toCharArray();
    Map<Character, Character> map = new HashMap<>();

    for (int i = 0; i < p.length - 1; i += 2) 
      map.put(p[i + 1], p[i]);

    Stack<Character> stack = new Stack<>();

    for (char c : s.toCharArray()) {
      if (c == '(' || c == '{' || c == '[')
        stack.push(c);
      else if (stack.isEmpty() || stack.peek() != map.get(c))
        return false;
      else
        stack.pop();
    }

    return stack.isEmpty();
  }
}
```