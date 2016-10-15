# Range Sum Query - Immutable

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

**Example:**
```
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

**Note:**

1. You may assume that the array does not change.
2. There are many calls to sumRange function.

**Solution:**
```java
public class NumArray {
  int[] sums;

  public NumArray(int[] nums) {
    sums = new int[nums.length];

    for (int i = 0; i < nums.length; i++)
      sums[i] = nums[i] + ((i > 0) ? sums[i - 1] : 0);
  }

  public int sumRange(int i, int j) {
    return (i == 0) ? sums[j] : sums[j] - sums[i - 1];
  }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.sumRange(1, 2);
```