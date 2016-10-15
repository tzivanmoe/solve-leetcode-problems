# Multiply Strings

Given two numbers represented as strings, return multiplication of the numbers as a string.

**Note:**

* The numbers can be arbitrarily large and are non-negative.
* Converting the input string to integer is **NOT** allowed.
* You should **NOT** use internal library such as **BigInteger**.

**Solution:**
```java
public class Solution {
  public String multiply(String num1, String num2) {
    if (num1 == null || num2 == null || num1.length() == 0 || num2.length() == 0) {
      return "";
    }

    char[] chs1 = num1.toCharArray();
    char[] chs2 = num2.toCharArray();

    reverse(chs1, 0, chs1.length - 1);
    reverse(chs2, 0, chs2.length - 1);

    int n = chs1.length;
    int m = chs2.length;

    // total length won't be longer than m + n
    int[] res = new int[m + n];

    for (int i = 0; i < n; i++) {
      int val = 0;
      int d1 = (int)(chs1[i] - '0');

      for (int j = 0; j < m; j++) {
        int d2 = (int)(chs2[j] - '0');

        val = d1 * d2 + res[i + j] + val;
        res[i + j] = val % 10;
        val /= 10;
      }

      if (val > 0) {
        res[i + m] = val;
      }
    }

    StringBuilder sb = new StringBuilder();
    boolean valid = false;

    for (int i = res.length - 1; i >= 0; i--) {
      // ignore leading zeros
      if (!valid && res[i] == 0) {
        continue;
      }

      valid = true;
      sb.append(res[i]);
    }

    if (sb.length() == 0) {
        return "0";
    }

    return sb.toString();
  }

  void reverse(char[] chs, int lo, int hi) {
    while (lo < hi) {
      swap(chs, lo++, hi--);
    }
  }

  void swap(char[] chs, int i, int j) {
    char ch = chs[i];
    chs[i] = chs[j];
    chs[j] = ch;
  }
}
```