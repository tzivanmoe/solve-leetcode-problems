# Walls and Gates

You are given a m x n 2D grid initialized with these three possible values.

1. `-1` - A wall or an obstacle.
2. `0` - A gate.
3. `INF` - Infinity means an empty room. We use the value `2^31 - 1 = 2147483647` to represent `INF` as you may assume that the distance to a gate is less than `2147483647`.

Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with `INF`.

For example, given the 2D grid:
```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```
After running your function, the 2D grid should be:
```
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```

**Solution:**
```java
public class Solution {
  int[] dx = {-1, 1, 0, 0};
  int[] dy = {0, 0, -1, 1};

  public void wallsAndGates(int[][] rooms) {
    if (rooms.length == 0 || rooms[0].length == 0)
      return;

    int n = rooms.length, m = rooms[0].length;

    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        if (rooms[i][j] == 0) {
          bfs(rooms, n, m, i, j);
        }
      }
    }
  }

  void bfs(int[][] rooms, int n, int m, int i, int j) {
    Queue<Integer[]> queue = new LinkedList<>();
    queue.add(new Integer[]{i, j});
    queue.add(null);

    int level = 1;

    while (!queue.isEmpty()) {
      Integer[] p = queue.poll();

      if (p != null) {
        for (int k = 0; k < 4; k++) {
          int x = p[0] + dx[k];
          int y = p[1] + dy[k];

          if (x >= 0 && x < n && y >= 0 && y < m && rooms[x][y] > level) {
            rooms[x][y] = level;
            queue.add(new Integer[]{x, y});
          }
        }
      } else if (!queue.isEmpty()) {
        level++;
        queue.add(null);
      }
    }
  }
}
```