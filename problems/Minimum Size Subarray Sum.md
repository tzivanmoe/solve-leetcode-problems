# Minimum Size Subarray Sum

Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return 0 instead.

For example, given the array `[2,3,1,2,4,3]` and s = `7`,
the subarray `[4,3]` has the minimal length under the problem constraint.

**More practice:**

If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).

**Solution:**
```java
public class Solution {
  public int minSubArrayLen(int s, int[] a) {
    if (a == null || a.length == 0)
      return 0;
        
    // i is slow pointer, j is fast pointer
    int i = 0, j = 0, sum = 0, min = Integer.MAX_VALUE;
        
    while (j < a.length) {
      sum += a[j++];
            
      while (sum >= s) {
        min = Math.min(min, j - i);
        sum -= a[i++];
      }
    }
        
    return min == Integer.MAX_VALUE ? 0 : min;
  }
}
```