# Remove Duplicates from Sorted Array II

Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = `[1,1,1,2,2,3]`,

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.

**Solution:**
```java
public class Solution {
  public int removeDuplicates(int[] nums) {
    if (nums == null) return 0;
    if (nums.length < 3) return nums.length;
        
    int n = nums.length;
        
    int i = 2;
        
    for (int j = 2; j < n; j++) {
      if (nums[j] != nums[i - 2]) {
        nums[i++] = nums[j];
      }
    }
        
    return i;
  }
}
```