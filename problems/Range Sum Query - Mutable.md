# Range Sum Query - Mutable

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.

**Example:**
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

**Note:**

1. The array is only modifiable by the update function.
2. You may assume the number of calls to update and sumRange function is distributed evenly.

**Solution:**
```java
public class NumArray {
  int[] arr;    // stores nums[]
  int[] BITree; // binary indexed tree

  public NumArray(int[] nums) {
    int n = nums.length;
    arr = new int[n];
    BITree = new int[n + 1];

    for (int i = 0; i < n; i++) {
      update(i, nums[i]); // init BITree[]
      arr[i] = nums[i];   // init arr[]
    }
  }

  void update(int i, int val) {
    int diff = val - arr[i]; // get the diff
    arr[i] = val;            // update arr[]

    i++;
    while (i <= arr.length) {
      BITree[i] += diff; // update BITree[]
      i += i & (-i);     // update index to that of parent
    }
  }

  int getSum(int i) {
    int sum = 0;

    i++;
    while (i > 0) {
      sum += BITree[i]; // accumulate the sum
      i -= i & (-i);    // move index to parent node
    }
    return sum;
  }

  public int sumRange(int i, int j) {
    return getSum(j) - getSum(i - 1);
  }
}

// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.update(1, 10);
// numArray.sumRange(1, 2);
```