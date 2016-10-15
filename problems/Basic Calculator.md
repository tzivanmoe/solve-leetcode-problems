# Basic Calculator

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, non-negative integers and empty spaces .

You may assume that the given expression is always valid.

Some examples:
```
"1 + 1" = 2
" 2-1 + 2 " = 3
"(1+(4+5+2)-3)+(6+8)" = 23
````

**Note:** Do not use the eval built-in library function.

**Solution:**
```java
public class Solution {
  public int calculate(String s) {
    char[] a = s.toCharArray();

    Stack<Integer> stack = new Stack<Integer>();
    stack.push(1);

    int res = 0;
    int sign = 1;

    for (int i = 0; i < a.length; i++) {
      if (a[i] == ')') {
        stack.pop();
      } else if (a[i] == '+') {
        sign = 1;
      } else if (a[i] == '-') {
        sign = -1;
      } else if (a[i] == '(') {
        stack.push(stack.peek() * sign);
        sign = 1;
      } else if (Character.isDigit(a[i])) {
        int tmp = a[i] - '0';

        while (i + 1 < s.length() && Character.isDigit(a[i + 1]))
          tmp = tmp * 10 + a[++i] - '0';

        res += sign * stack.peek() * tmp;
      }
    }

    return res;
  }
}
```