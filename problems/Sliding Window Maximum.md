# Sliding Window Maximum

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

For example,

Given nums = `[1,3,-1,-3,5,3,6,7]`, and `k = 3`.

```
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

Therefore, return the max sliding window as `[3,3,5,5,6,7]`.

**Note: **

You may assume k is always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

**Follow up:**

Could you solve it in linear time?

**Hint:**

1. How about using a data structure such as deque (double-ended queue)?
2. The queue size need not be the same as the window’s size.
3. Remove redundant elements and the queue should store only elements that need to be considered.

**Solution:**
```java
public class Solution {
  public int[] maxSlidingWindow(int[] nums, int w) {
    if (nums == null || nums.length == 0 || w < 1)
      return new int[0];

    int n = nums.length, k = 0;
    int[] res = new int[n - w + 1];

    // use a deque to control the window
    Deque<Integer> q = new ArrayDeque<Integer>();

    for (int i = 0; i < n; i++) {
      // exceeds window size
      if (!q.isEmpty() && q.peekFirst() + w <= i)
        q.removeFirst();

      // pop those smaller ones from behind
      while (!q.isEmpty() && nums[q.peekLast()] <= nums[i])
        q.removeLast();

      q.addLast(i);

      if (i >= w - 1)
        res[k++] = nums[q.peekFirst()];
    }

    return res;
  }
}
```