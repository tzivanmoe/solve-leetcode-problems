# Reverse Words in a String II

Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

For example,

Given s = `"the sky is blue"`,

return `"blue is sky the"`.

Could you do it in-place without allocating extra space?

Related problem: Rotate Array

**Solution:**
```java
public class Solution {
  public void reverseWords(char[] chars) {
    int n = chars.length;

    // step 1. reverse the whole string
    reverse(chars, 0, n - 1);

    // step 2. reverse each word
    int i = 0, j = 0;

    while (i < n) {
      // trim the space in front
      while (i < n && chars[i] == ' ') { i++; }
      j = i;

      // find the border
      while (j < n && chars[j] != ' ') { j++; }

      // reverse from i to j - 1
      reverse(chars, i, j - 1);

      // continue
      i = j;
    }
  }

  private void reverse(char[] chars, int start, int end) {
    while (start < end) {
      char tmp = chars[start];
      chars[start] = chars[end];
      chars[end] = tmp;

      start++;
      end--;
    }
  }
}
```