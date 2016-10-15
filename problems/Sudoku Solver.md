# Sudoku Solver

Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character `'.'`.

You may assume that there will be only one unique solution.

![](250px-Sudoku-by-L2G-20050714.svg.png)

A sudoku puzzle...

![](250px-Sudoku-by-L2G-20050714_solution.svg.png)

...and its solution numbers marked in red.

**Solution:**
```java
public class Solution {
  public void solveSudoku(char[][] board) {
    if (board == null || board.length != 9 || board[0].length != 9) {
      return;
    }
    solve(board, 0, 0);
  }
    
  private boolean solve(char[][] board, int i, int j) {
    if (j == 9) {
      return solve(board, i + 1, 0);
    }
      
    if (i == 9) {
      return true;
    }
      
    if (board[i][j] != '.') {
      return solve(board, i, j + 1);
    }
      
    // try 1 - 9
    for (int k = 1; k <= 9; k++) {
      board[i][j] = (char)('0' + k);
        
      if (check(board, i, j)) {
        if (solve(board, i, j + 1)) {
          return true;
        }
      }
        
      board[i][j] = '.';
    }
      
    return false;
  }
    
  private boolean check(char[][] board, int i, int j) {
    // check row i
    for (int k = 0; k < 9; k++) {
      if (k != j && board[i][k] == board[i][j]) {
        return false;
      }
    }
      
    // check column j
    for (int k = 0; k < 9; k++) {
      if (k != i && board[k][j] == board[i][j]) {
        return false;
      }
    }
      
    // check grid
    int row = i/3 * 3;
    int col = j/3 * 3;
      
    for (int r = row; r < row + 3; r++) {
      for (int c = col; c < col + 3; c++) {
        if (r != i && c != j && board[r][c] == board[i][j]) {
          return false;
        }
      }
    }
      
    return true;
  }
}
```
