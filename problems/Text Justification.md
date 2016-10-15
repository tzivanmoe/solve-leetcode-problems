# Text Justification

Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

**For example,**

**words:** `["This", "is", "an", "example", "of", "text", "justification."]`

**L:** `16`.

Return the formatted lines as:
```
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

**Note:** Each word is guaranteed not to exceed L in length.

**Solution:**
```java
public class Solution {
  public List<String> fullJustify(String[] words, int maxWidth) {
    List<String> res = new ArrayList<>();

    int n = words.length, i = 0;

    while (i < n) {
      int j = i, len = -1;

      while (j < n && len + words[j].length() + 1 <= maxWidth) {
        len += words[j].length() + 1;
        j++;
      }

      int space = 1, extra = 0;

      if (j != i + 1 && j != n) {
        space = (maxWidth - len) / (j - i - 1) + 1;
        extra = (maxWidth - len) % (j - i - 1);
      }

      StringBuilder sb = new StringBuilder();

      sb.append(words[i]);

      for (int k = i + 1; k < j; k++) {
        for (int s = space; s > 0; s--) {
          sb.append(' ');
        }

        if (extra-- > 0) {
          sb.append(' ');
        }

        sb.append(words[k]);
      }

      int left = maxWidth - sb.length();

      while (left-- > 0) {
        sb.append(' ');
      }

      res.add(sb.toString());

      i = j;
    }

    return res;
  }
}
```