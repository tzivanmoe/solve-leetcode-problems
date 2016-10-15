# Valid Sudoku

Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

![](250px-Sudoku-by-L2G-20050714.svg.png)

A partially filled sudoku which is valid.

**Note:**

A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

**Solution:**
```java
public class Solution {
  public boolean isValidSudoku(char[][] board) {
    int n = board.length, m = board[0].length;

    if (n != 9 || m != 9)
      return false;

    // check rows
    for (int i = 0; i < 9; i++) {
      Set<Character> set = new HashSet<Character>();

      for (int j = 0; j < 9; j++) {
        char c = board[i][j];
        if (c != '.') {
          if (set.contains(c)) return false;
          set.add(c);
        }
      }
    }

    // check columns
    for (int j = 0; j < 9; j++) {
      Set<Character> set = new HashSet<Character>();

      for (int i = 0; i < 9; i++) {
        char c = board[i][j];
        if (c != '.') {
          if (set.contains(c)) return false;
          set.add(c);
        }
      }
    }

    // check grids
    for (int k = 0; k < 9; k++) {
      int row = k / 3 * 3;
      int col = k % 3 * 3;

      Set<Character> set = new HashSet<Character>();

      for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
          char c = board[row + i][col + j];
          if (c != '.') {
            if (set.contains(c)) return false;
            set.add(c);
          }
        }
      }
    }

    return true;
  }
}
```
