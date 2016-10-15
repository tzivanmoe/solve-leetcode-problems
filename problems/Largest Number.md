# Largest Number

Given a list of non negative integers, arrange them such that they form the largest number.

For example, given `[3, 30, 34, 5, 9]`, the largest formed number is `9534330`.

Note: The result may be very large, so you need to return a string instead of an integer.

**Solution:**
```java
public class Solution {
  public String largestNumber(int[] num) {
    int n = num.length;

    Integer[] A = new Integer[n];
    for (int i = 0; i < n; i++) {
      A[i] = Integer.valueOf(num[i]);
    }

    // sort the array by string
    Arrays.sort(A, new Comparator<Integer>() {
      @Override
      public int compare(Integer a, Integer b) {
        String stra = String.valueOf(a);
        String strb = String.valueOf(b);

        return (strb + stra).compareTo(stra + strb);
      }
    });

    StringBuilder sb = new StringBuilder();

    for (int i = 0; i < n; i++) {
      if (A[i] == 0 && sb.length() == 0) {
        continue;
      }

      sb.append(String.valueOf(A[i]));
    }

    if (sb.length() == 0) {
      return "0";
    }

    return sb.toString();
  }
}
```