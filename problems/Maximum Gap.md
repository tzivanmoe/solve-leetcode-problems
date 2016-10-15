# Maximum Gap

Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

Try to solve it in linear time/space.

Return 0 if the array contains less than 2 elements.

You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.

**Solution:**
```java
public class Solution {
  public int maximumGap(int[] nums) {
      if (nums == null || nums.length < 2) {
        return 0;
      }

      int n = nums.length;

      // m is the maximal number in nums
      int m = nums[0];
      for (int i = 1; i < n; i++) {
        m = Math.max(m, nums[i]);
      }

      int exp = 1; // 1, 10, 100, 1000 ...
      int R = 10; // 10 digits

      int[] aux = new int[n];

      while (m / exp > 0) { // Go through all digits from LSB to MSB
        int[] count = new int[R];

        for (int i = 0; i < n; i++) {
          count[(nums[i] / exp) % 10]++;
        }

        for (int i = 1; i < R; i++) {
          count[i] += count[i - 1];
        }

        for (int i = n - 1; i >= 0; i--) {
          aux[--count[(nums[i] / exp) % 10]] = nums[i];
        }

        for (int i = 0; i < n; i++) {
            nums[i] = aux[i];
        }

        exp *= 10;
      }

      int max = 0;
      for (int i = 1; i < aux.length; i++) {
        max = Math.max(max, aux[i] - aux[i - 1]);
      }

      return max;
  }
}
```