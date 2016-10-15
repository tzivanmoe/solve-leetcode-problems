# Contains Duplicate

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Solution:**
```java
public class Solution {
  public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<>();
        
    for (int i = 0; i < nums.length; i++) {
      int num = nums[i];
            
      if (!set.contains(num)) {
        set.add(num);
      } else {
        return true;
      }
    }
        
    return false;
  }
}
```