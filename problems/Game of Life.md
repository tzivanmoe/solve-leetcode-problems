# Game of Life

According to the [Wikipedia's article](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life): "The **Game of Life**, also known simply as **Life**, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its [eight neighbors](https://en.wikipedia.org/wiki/Moore_neighborhood) (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. 
Any live cell with fewer than two live neighbors dies, as if caused by under-population.
2. 
Any live cell with two or three live neighbors lives on to the next generation.
3. 
Any live cell with more than three live neighbors dies, as if by over-population..
4. 
Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state (after one update) of the board given its current state.

**Follow up:**
1. 
Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. 
In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

**Solution:**
```java
public class Solution {
  public void gameOfLife(int[][] board) {
    int n = board.length, m = board[0].length;
        
    int[] di = {-1, -1, -1,  0, 0,  1, 1, 1};
    int[] dj = {-1,  0,  1, -1, 1, -1, 0, 1};
        
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {
        int live = 0;
                
        for (int k = 0; k < 8; k++) {
          int ii = i + di[k], jj = j + dj[k];
                    
          if (ii < 0 || ii >= n || jj < 0 || jj >= m)
            continue;
                        
          if (board[ii][jj] == 1 || board[ii][jj] == 2) 
            live++;
        }
                
        if (board[i][j] == 1 && (live < 2 || live > 3)) {
          board[i][j] = 2;
        } else if (board[i][j] == 0 && live == 3) { 
          board[i][j] = 3;
        }
      }
    }
        
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) { 
        board[i][j] %= 2;
      }
    }
  }
}
```