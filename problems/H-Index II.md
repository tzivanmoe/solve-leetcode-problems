# H-Index II

Follow up for H-Index: What if the citations array is sorted in ascending order? Could you optimize your algorithm?

**Hint:**

Expected runtime complexity is in O(log n) and the input is sorted.

**Solution:**
```java
public class Solution {
  public int hIndex(int[] citations) {
    int n = citations.length;
    int lo = 0, hi = n - 1;

    while (lo <= hi) {
      int mid = lo + (hi - lo) / 2;

      if (citations[mid] >= n - mid) {
        hi = mid - 1;
      } else {
        lo = mid + 1;
      }
    }

    return n - 1 - hi;
  }
}
```