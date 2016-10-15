# Palindrome Number

Determine whether an integer is a palindrome. Do this without extra space.

**Some hints:**

Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

**Solution:**
```java
public class Solution {
  public boolean isPalindrome(int x) {
    if (x < 0)
      return false;

    int s = 0, y = x;

    while (x > 0) {
      s = s * 10 + x % 10;
      x /= 10;
    }

    return s == y;
  }
}
```