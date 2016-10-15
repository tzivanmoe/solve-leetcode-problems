# Compare Version Numbers

Compare two version numbers version1 and version2.
If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the `.` character.
The `.` character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:
```
0.1 < 1.1 < 1.2 < 13.37
```

**Solution:**
```java
public class Solution {
  public int compareVersion(String version1, String version2) {
    char[] c1 = version1.toCharArray();
    char[] c2 = version2.toCharArray();

    int i = 0, j = 0, v1 = 0, v2 = 0, n1 = c1.length, n2 = c2.length;

    while (i < n1 && j < n2) {
      // get version number v1 and v2
      while (i < n1 && Character.isDigit(c1[i])) 
        v1 = v1 * 10 + c1[i++] - '0';

      while (j < n2 && Character.isDigit(c2[j])) 
        v2 = v2 * 10 + c2[j++] - '0';

      if (v1 > v2) return 1;
      if (v2 > v1) return -1;

      // reset version numbers
      v1 = 0; v2 = 0;

      // skip '.'
      i++; j++;
    }

    while (i < n1 && Character.isDigit(c1[i])) 
      v1 = v1 * 10 + c1[i++] - '0';

    while (j < n2 && Character.isDigit(c2[j])) 
      v2 = v2 * 10 + c2[j++] - '0';

    if (v1 > v2) return 1;
    if (v1 < v2) return -1;

    return 0;
  }
}
```