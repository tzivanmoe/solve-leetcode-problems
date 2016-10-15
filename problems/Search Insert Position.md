# Search Insert Position

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.

`[1,3,5,6]`, 5 → 2

`[1,3,5,6]`, 2 → 1

`[1,3,5,6]`, 7 → 4

`[1,3,5,6]`, 0 → 0

**Solution:**
```java
public class Solution {
  public int searchInsert(int[] nums, int target) {
    return search(nums, target, 0, nums.length - 1);
  }
    
  int search(int[] nums, int target, int lo, int hi) {
    if (lo > hi) {
      return lo;
    }
        
    int mid = lo + (hi - lo) / 2;
        
    if (nums[mid] == target) {
      return mid;
    }
        
    if (target < nums[mid]) {
      return search(nums, target, lo, mid - 1);
    } else {
      return search(nums, target, mid + 1, hi);
    }
  }
}
```