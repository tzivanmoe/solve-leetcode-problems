# Number of Islands II

A 2d grid map of `m` rows and `n` columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, **count the number of islands after each addLand operation**. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example:**

Given `m = 3, n = 3`, `positions = [[0,0], [0,1], [1,2], [2,1]]`.

Initially, the 2d grid `grid` is filled with water. (Assume 0 represents water and 1 represents land).
```
0 0 0
0 0 0
0 0 0
```
Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.
```
1 0 0
0 0 0   Number of islands = 1
0 0 0
```
Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.
```
1 1 0
0 0 0   Number of islands = 1
0 0 0
```
Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.
```
1 1 0
0 0 1   Number of islands = 2
0 0 0
```
Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.
```
1 1 0
0 0 1   Number of islands = 3
0 1 0
```
We return the result as an array: `[1, 1, 2, 3]`

**Challenge:**

Can you do it in time complexity O(k log mn), where k is the length of the `positions`?

**Solution:**
```java
public class Solution {
  int[] dx = {-1, 1, 0, 0};
  int[] dy = {0, 0, -1, 1};
    
  public List<Integer> numIslands2(int m, int n, int[][] positions) {
    List<Integer> res = new ArrayList<>();
      
    int count = 0;
    int[] nums = new int[m*n];
    Arrays.fill(nums, -1);

    for (int[] p : positions) {
      // for each position, mark it as new island
      int x = p[0]*n + p[1];
      nums[x] = x;
      count++;
        
      for (int i = 0; i < 4; i++) {
        // check neighbours
        int nx = p[0] + dx[i];
        int ny = p[1] + dy[i];
        int y = nx*n + ny;
          
        // ignore invalid position
        if (nx < 0 || nx >= m || ny < 0 || ny >= n || nums[y] == -1) { 
          continue;
        }
          
        // find and union islands
        y = find(nums, y);
        x = find(nums, x);
        nums[y] = x;
          
        // merge two isolated islands
        if (y != x) {
          count--;
        }
      }
        
      res.add(count);
    }

    return res;
  }
    
  int find(int nums[], int i) {
    if (nums[i] == i) {
      return i;
    }
      
    nums[i] = find(nums, nums[i]);
    return nums[i];
  }
}
```