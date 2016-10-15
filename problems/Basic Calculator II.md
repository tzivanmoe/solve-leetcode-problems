# Basic Calculator II

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, `+`, `-`, `*`, `/` operators and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid.

Some examples:
```
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5
```

**Note**: **Do not** use the `eval` built-in library function.

**Solution:**
```java
public class Solution {
  public int calculate(String s) {
    if (s == null || s.length() == 0)
      return 0;

    s = "+" + s + "+";
    char sign = '+';
    char[] a = s.toCharArray();
    int n = s.length(), res = 0, num = 0;
    Stack<Integer> stack = new Stack<Integer>();

    for (int i = 0; i < n; i++) {
      if (Character.isDigit(a[i]))
        num = num * 10 + a[i] - '0';

      if (isOperator(a[i])) {
        if (sign == '+') stack.push(num);
        if (sign == '-') stack.push(-num);
        if (sign == '*') stack.push(stack.pop() * num);
        if (sign == '/') stack.push(stack.pop() / num);

        num = 0;

        sign = a[i];
      }
    }

    for (int i : stack) 
      res += i;

    return res;
  }

  boolean isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
  }
}
```