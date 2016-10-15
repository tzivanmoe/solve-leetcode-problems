# Find Peak Element

A peak element is an element that is greater than its neighbors.

Given an input array where `num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1] = num[n] = -∞`.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

**Note:**

Your solution should be in logarithmic complexity.

**Solution:**
```java
public class Solution {
  public int findPeakElement(int[] nums) {
    return search(nums, 0, nums.length - 1);
  }
    
  int search(int[] a, int lo, int hi) {
    if (lo > hi) {
      return -1;
    }
            
    int mid = lo + (hi - lo) / 2;
        
    if ((mid == 0 || a[mid - 1] < a[mid]) && (mid == a.length - 1 || a[mid] > a[mid + 1])) {
      return mid;
    }
            
    if (a[mid] < a[mid + 1]) {
      return search(a, mid + 1, hi);
    } else {
      return search(a, lo, mid - 1);
    }
  }
}
```