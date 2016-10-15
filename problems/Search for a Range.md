# Search for a Range

Given a sorted array of integers, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return `[-1, -1]`.

For example,

Given `[5, 7, 7, 8, 8, 10]` and target value 8,
return `[3, 4]`.

**Solution:**
```java
public class Solution {
  public int[] searchRange(int[] nums, int target) {
    int lo = lower(nums, target, 0, nums.length - 1);
        
    if (lo == -1) {
      return new int[] {-1, -1};
    }
        
    int hi = upper(nums, target, 0, nums.length - 1);
        
    return new int[] {lo, hi};
  }
    
  int lower(int[] nums, int target, int lo, int hi) {
    if (lo > hi) {
      return -1;
    }
        
    int mid = lo + (hi - lo) / 2;
        
    if (nums[mid] == target && (mid == 0 || nums[mid - 1] < target)) {
      return mid;
    }
        
    if (nums[mid] >= target) {
      return lower(nums, target, lo, mid - 1);
    } else {
      return lower(nums, target, mid + 1, hi);
    }
  }
    
  int upper(int[] nums, int target, int lo, int hi) {
    if (lo > hi) {
      return -1;
    }
        
    int mid = lo + (hi - lo) / 2;
        
    if (nums[mid] == target && (mid == nums.length - 1 || target < nums[mid + 1])) {
      return mid;
    }
        
    if (nums[mid] <= target) {
      return upper(nums, target, mid + 1, hi);
    } else {
      return upper(nums, target, lo, mid - 1);
    }
  }
}
```