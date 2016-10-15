# Contains Duplicate III

Given an array of integers, find out whether there are two distinct indices i and j in the array such that the difference between nums[i] and nums[j] is at most t and the difference between i and j is at most k.

**Solution:**
```java
public class Solution {
  public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    TreeSet<Integer> tree = new TreeSet<>();

    for (int i = 0; i < nums.length; i++) {
      Integer ceil = tree.ceiling(nums[i] - t);
      Integer floor = tree.floor(nums[i] + t);

      if ((ceil != null && ceil <= nums[i]) || (floor != null && floor >= nums[i])) {
        return true;
      }

      tree.add(nums[i]);

      if (i >= k) {
        tree.remove(nums[i - k]);
      }
    }

    return false;
  }
}
```