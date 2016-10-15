# 3Sum


Given an array *S* of *n* integers, are there elements *a*, *b*, *c* in *S* such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:** The solution set must not contain duplicate triplets.

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

**Solution:**

```java
public class Solution {
  
  public List<List<Integer>> threeSum(int[] num) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    
    Set<String> set = new HashSet<String>();
    
    Arrays.sort(num);
    
    int n = num.length;
    
    for (int i = 0; i < n - 2; i++) {
      int j = i + 1, k = n - 1;
      
      while (j < k) {
        int sum = num[i] + num[j] + num[k];
        
        if (sum == 0) {
          String key = String.format("%d,%d,%d", num[i], num[j], num[k]);
          
          if (!set.contains(key)) {
            set.add(key);
            
            List<Integer> sol = new ArrayList<Integer>();
            sol.add(num[i]);
            sol.add(num[j]);
            sol.add(num[k]);
            
            res.add(sol);
          }
          
          j++;
          k--;
        } else if (sum < 0) {
          j++;
        } else {
          k--;
        }
      }
    }
    
    return res;
  }

}
```

Time complexity: O(n^2)