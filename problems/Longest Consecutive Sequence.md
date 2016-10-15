# Longest Consecutive Sequence

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given `[100, 4, 200, 1, 3, 2]`,
The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.

Your algorithm should run in *O(n)* complexity.

**Solution:**
```java
public class Solution {
  public int longestConsecutive(int[] nums) {
    int max = 0;
        
    Set<Integer> set = new HashSet<Integer>();
        
    for (int i = 0; i < nums.length; i++) {
      set.add(nums[i]);   
    }
        
    for (int i = 0; i < nums.length; i++) {
      int count = 1;
            
      // look left
      int num = nums[i];
      while (set.contains(--num)) {
        count++;
        set.remove(num);
      }
            
      // look right
      num = nums[i];
      while (set.contains(++num)) {
        count++;
        set.remove(num);
      }
            
      max = Math.max(max, count);
    }
        
    return max;
  }
}
```