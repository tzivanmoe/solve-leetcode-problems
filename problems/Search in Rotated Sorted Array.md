# Search in Rotated Sorted Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

**Solution:**
```java
public class Solution {
  public int search(int[] nums, int target) {
    int n = nums.length;
        
    return search(nums, 0, n - 1, target);
  }
    
  int search(int[] nums, int lo, int hi, int target) {
    if (lo > hi)
      return -1;
            
    int mid = lo + (hi - lo) / 2;
        
    if (nums[mid] == target) {
      return mid;
    }
        
    if (nums[lo] <= nums[mid]) {
      if (nums[lo] <= target && target < nums[mid]) {
        return search(nums, lo, mid - 1, target);
      } else {
        return search(nums, mid + 1, hi, target);
      }
    } else {
      if (nums[mid] < target && target <= nums[hi]) {
        return search(nums, mid + 1, hi, target);
      } else {
        return search(nums, lo, mid - 1, target);
      }
    }
  }
}
```