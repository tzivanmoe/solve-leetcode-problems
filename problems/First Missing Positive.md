# First Missing Positive

Given an unsorted integer array, find the first missing positive integer.

For example,

Given `[1,2,0]` return `3`,
and `[3,4,-1,1]` return `2`.

Your algorithm should run in *O(n)* time and uses constant space.

**Solution:**
```java
public class Solution {
  public int firstMissingPositive(int[] a) {
    int i = 0;
    while (i < a.length) {
      if (a[i] > 0 && a[i] <= a.length && a[i] != a[a[i] - 1]) {
        swap(a, i, a[i] - 1);
      } else {
        i++;
      }
    }
        
    i = 0;
    while (i < a.length && a[i] == i + 1) {
      i++;
    }
        
    return i + 1;
  }
    
  void swap(int[] a, int i, int j) {
    int b = a[i];
    a[i] = a[j];
    a[j] = b;
  }
}
```