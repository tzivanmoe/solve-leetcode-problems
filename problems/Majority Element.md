# Majority Element

Given an array of size n, find the majority element. The majority element is the element that appears more than `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Solution:**
```java
public class Solution {
  public int majorityElement(int[] nums) {
    Integer m = null;
    int c = 0;
        
    for (int i = 0; i < nums.length; i++) {
      if (m != null && m == nums[i]) {
        c++;
      } else if (c == 0) {
        m = nums[i];
        c = 1;
      } else {
        c--;
      }
    }
        
    c = 0;
    for (int i = 0; i < nums.length; i++) {
      if (m != null && m == nums[i]) {
        c++;
      }
    }
        
    if (c > nums.length / 2) {
      return m;
    } else {
      return -1;
    }
  }
}
```