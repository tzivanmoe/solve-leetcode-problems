# Find Minimum in Rotated Sorted Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

Find the minimum element.

You may assume no duplicate exists in the array.

**Solution:**
```java
public class Solution {
  public int findMin(int[] a) {
    return search(a, 0, a.length - 1);
  }
    
  int search(int[] a, int lo, int hi) {
    // a[] is sorted
    if (lo > hi) {
      return a[0];
    }
            
    int mid = lo + (hi - lo) / 2;
        
    if (mid > 0 && a[mid - 1] > a[mid]) {
      return a[mid];
    }
        
    if (mid < a.length - 1 && a[mid] > a[mid + 1]) {
      return a[mid + 1];
    }
            
    if (a[mid] < a[hi]) {
      return search(a, lo, mid - 1);
    } else {
      return search(a, mid + 1, hi);
    }
  }
}
```