# Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,

Given board =
```
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```
word = `"ABCCED"`, -> returns `true`,
word = `"SEE"`, -> returns `true`,
word = `"ABCB"`, -> returns `false`.

**Solution:**
```java
public class Solution {
  int[] dx = {-1, 1, 0, 0};
  int[] dy = {0, 0, -1, 1};
    
  public boolean exist(char[][] board, String word) {
    int n = board.length;
    int m = board[0].length;
        
    boolean[][] used = new boolean[n][m];
        
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        if (search(board, n, m, i, j, used, 0, word)) {
          return true;
        }
      }
    }
        
    return false;
  }
    
  boolean search(char[][] board, int n, int m, int i, int j, boolean[][] used, int k, String word) {
    if (k == word.length()) {
      return true;
    }
        
    if (i < 0 || i >= n || j < 0 || j >= m) {
      return false;
    }
        
    if (board[i][j] != word.charAt(k)) {
      return false;
    }
        
    if (used[i][j]) {
      return false;
    }
        
    used[i][j] = true;
        
    boolean res = false;
        
    for (int d = 0; d < 4; d++) {
      if (search(board, n, m, i + dx[d], j + dy[d], used, k + 1, word)) {
        res = true;
        break;
      }
    }
        
    used[i][j] = false;
        
    return res;
  }
}
```