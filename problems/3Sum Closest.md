# 3Sum Closest

Given an array *S* of *n* integers, find three integers in *S* such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

**Solution:**

```java
public class Solution {
    public int threeSumClosest(int[] num, int target) {
        Arrays.sort(num);
        
        int n = num.length;
        int closest = num[0] + num[1] + num[2];
        
        for (int i = 0; i < n - 2; i++) {
            int j = i + 1;
            int k = n - 1;
            
            while (j < k) {
                int sum = num[i] + num[j] + num[k];
                
                if (sum == target) {
                    return sum;
                } else if (sum < target) {
                    j++;
                } else {
                    k--;
                }
                
                if (Math.abs(target - sum) < Math.abs(target - closest)) {
                    closest = sum;
                }
            }
        }
        
        return closest;
    }
}
```

Time complexity: O(n^2)