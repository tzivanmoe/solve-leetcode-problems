# ZigZag Conversion

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```

`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

**Solution:**
```java
public class Solution {
  public String convert(String s, int nRows) {
    if (nRows == 1) 
      return s;

    List<StringBuilder> list = new ArrayList<>();

    for (int i = 0; i < nRows; i++) {
      list.add(new StringBuilder());
    }

    int row = 0, dir = 0;
    for (int i = 0; i < s.length(); i++) {
      list.get(row).append(s.charAt(i));

      if (row == 0) dir = 1;
      if (row == nRows - 1) dir = -1;

      row += dir;
    }

    StringBuilder res = new StringBuilder();
    for (StringBuilder sb : list) {
      res.append(sb.toString());
    }
    return res.toString();
  }
}
```