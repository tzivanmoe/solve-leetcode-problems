# Excel Sheet Column Title

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

**Solution:**
```java
public class Solution {
  public String convertToTitle(int n) {
    String res = "";

    while (n >= 1) {
      res = (char)('A' + (n - 1) % 26) + res;
      n = (n - 1) / 26;
    }

    return res;
  }
}
```