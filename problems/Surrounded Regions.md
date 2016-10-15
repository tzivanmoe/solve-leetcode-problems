# Surrounded Regions

Given a 2D board containing `'X'` and `'O'`, capture all regions surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

For example,
```
X X X X
X O O X
X X O X
X O X X
```
After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```

**Solution:**
```java
public class Solution {
  int[] dx = {-1, 1, 0, 0};
  int[] dy = {0, 0, -1, 1};

  public void solve(char[][] board) {
    if (board == null || board.length == 0 || board[0].length == 0) return;

    int n = board.length;
    int m = board[0].length;

    // scan the borders and mark the 'O's to '1'
    for (int i = 0; i < n; i++)
      for (int j = 0; j < m; j++)
        if ((i == 0 || i == n - 1 || j == 0 || j == m - 1) && board[i][j] == 'O')
          bfs(board, n, m, i, j);

    // scan the inner area and mark the 'O's to 'X'
    for (int i = 1; i < n; i++)
      for (int j = 1; j < m; j++)
        if (board[i][j] == 'O')
          board[i][j] = 'X';

    // reset all the '1's to 'O's
    for (int i = 0; i < n; i++)
      for (int j = 0; j < m; j++)
        if (board[i][j] == '1')
          board[i][j] = 'O';

  }

  void bfs(char[][] board, int n, int m, int i, int j) {
    Queue<int[]> queue = new LinkedList<int[]>();
    queue.add(new int[]{i, j});

    board[i][j] = '1';

    while (!queue.isEmpty()) {
      int[] pos = queue.poll();

      for (int k = 0; k < 4; k++) {
        i = pos[0] + dx[k];
        j = pos[1] + dy[k];

        if (i >= 0 && i < n && j >= 0 && j < m && board[i][j] == 'O') {
          board[i][j] = '1';
          queue.add(new int[]{i, j});
        }
      }
    }
  }
}
```