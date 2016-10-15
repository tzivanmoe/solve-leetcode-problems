# Smallest Rectangle Enclosing Black Pixels

An image is represented by a binary matrix with `0` as a white pixel and `1` as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location `(x, y)` of one of the black pixels, return the area of the smallest (axis-aligned) rectangle that encloses all black pixels.

For example, given the following image:
```
[
  "0010",
  "0110",
  "0100"
]
```
and `x = 0`, `y = 2`,
Return `6`.

**Solution:**
```java
public class Solution {
  public int minArea(char[][] image, int x, int y) {
    int n = image.length, m = image[0].length;
    int x1 = x, y1 = y, x2 = x, y2 = y;

    int[] dx = {0, 0, -1, 1};
    int[] dy = {-1, 1, 0, 0};

    Queue<int[]> queue = new LinkedList<>();
    Set<Integer> visited = new HashSet<>();

    queue.add(new int[]{x, y});
    visited.add(x * m + y);

    while (!queue.isEmpty()) {
      int[] p = queue.poll();

      x = p[0]; y = p[1];

      if (x < x1) x1 = x;
      if (x > x2) x2 = x;

      if (y < y1) y1 = y;
      if (y > y2) y2 = y;

      for (int i = 0; i < 4; i++) {
        int nx = x + dx[i], ny = y + dy[i];

        if (nx < 0 || nx >= n || ny < 0 || ny >= m || image[nx][ny] != '1') {
          continue;
        }

        if (!visited.contains(nx * m + ny)) {
          queue.add(new int[]{nx, ny});
          visited.add(nx * m + ny);
        }
      }
    }

    return (x2 - x1 + 1) * (y2 - y1 + 1);
  }
}
```