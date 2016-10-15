# Triangle

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

**Note:**

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

**Solution:**
```java
public class Solution {
  public int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();
        
    int[] arr = new int[n];
        
    for (int i = 0; i < n; i++) {
      arr[i] = triangle.get(n - 1).get(i);
    }
        
    for (int i = n - 2; i >= 0; i--) {
      for (int j = 0; j <= i; j++) {
        arr[j] = Math.min(arr[j], arr[j + 1]) + triangle.get(i).get(j);
      }
    }
        
    return arr[0];
  }
}
```