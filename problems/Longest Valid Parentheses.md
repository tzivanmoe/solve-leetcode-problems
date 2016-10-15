# Longest Valid Parentheses

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

For `"(()"`, the longest valid parentheses substring is `"()"`, which has length = `2`.

Another example is `")()())"`, where the longest valid parentheses substring is `"()()"`, which has length = `4`.

**Solution:**
```java
public class Solution {
  public int longestValidParentheses(String s) {
      int i = -1, j = 0, max = 0;

      Stack<Integer> stack = new Stack<>();

      while (j < s.length()) {
      char c = s.charAt(j);

      if (c == '(') {
        stack.push(j);
      } else {
        if (stack.isEmpty()) {
          i = j;
        } else {
          stack.pop();
          max = Math.max(max, j - (stack.isEmpty() ? i : stack.peek()));
        }
      }

      j++;
    }

    return max;
  }
}
```