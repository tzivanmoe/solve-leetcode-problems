# Search in Rotated Sorted Array II

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.

**Solution:**
```java
public class Solution {
  public boolean search(int[] A, int target) {
    return bsearch(A, target, 0, A.length - 1);
  }
    
  private boolean bsearch(int[] A, int target, int lo, int hi) {
    if (lo > hi) {
      return false;
    }
        
    int mid = lo + (hi - lo) / 2;
        
    if (A[mid] == target) {
      return true;
    }
        
    if (A[lo] < A[mid]) {
      if (target >= A[lo] && target < A[mid]) {
        return bsearch(A, target, lo, mid - 1);
      } else {
        return bsearch(A, target, mid + 1, hi);
      }
    } else if (A[lo] > A[mid]) {
      if (target > A[mid] && target <= A[hi]) {
        return bsearch(A, target, mid + 1, hi);
      } else {
        return bsearch(A, target, lo, mid - 1);
      }
    } else {
      return bsearch(A, target, lo + 1, hi);
    }
  }
}
```