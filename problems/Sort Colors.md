# Sort Colors

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:**

You are not suppose to use the library's sort function for this problem.

**Follow up:**

A rather straight forward solution is a two-pass algorithm using counting sort.

First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?

**Solution:**
```java
public class Solution {
  public void sortColors(int[] nums) {
    if (nums == null) {
      return;
    }
        
    int n = nums.length;
    int i = -1, j = 0, k = n;
        
    while (j < k) {
      if (nums[j] == 1) {
        j++;
      } else if (nums[j] == 0) {
        swap(nums, ++i, j++);
      } else {
        swap(nums, --k, j);
      }
    }
  }
    
  void swap(int[] nums, int i, int j) {
    int tmp = nums[i];
    nums[i] = nums[j];
    nums[j] = tmp;
  }
}
```