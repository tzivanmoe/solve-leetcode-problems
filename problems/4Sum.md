# 4Sum

Given an array *S* of *n* integers, are there elements *a*, *b*, *c*, and *d* in *S* such that `a + b + c + d = target`? Find all unique quadruplets in the array which gives the sum of target.

**Note:** The solution set must not contain duplicate quadruplets.

```
For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

**Solution:**

```java
public class Solution {
  public List<List<Integer>> fourSum(int[] num, int target) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    Set<String> set = new HashSet<String>();
        
    if (num == null || num.length < 4) {
      return res;
    }
        
    Arrays.sort(num);
        
    int n = num.length;
        
    for (int i = 0; i < n - 3; i++) {
      for (int j = i + 1; j < n - 2; j++) {
        int m = j + 1;
        int k = n - 1;
                
        while (m < k) {
          int sum = num[i] + num[j] + num[m] + num[k];
                    
          if (sum == target) {
            String key = String.format("%d,%d,%d,%d", num[i], num[j], num[m], num[k]);
                        
            if (!set.contains(key)) {
              set.add(key);
                            
              List<Integer> sol = new ArrayList<Integer>();
              sol.add(num[i]);
              sol.add(num[j]);
              sol.add(num[m]);
              sol.add(num[k]);
              res.add(sol);
            }
                        
            m++;
            k--;
          } else if (sum < target) {
            m++;
          } else {
            k--;
          }
        }
      }
    }
        
    return res;
  }
}
```

Time complexity: O(n^3)