# N-Queens

The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

![](8-queens.png)

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.

For example,

There exist two distinct solutions to the 4-queens puzzle:
```
[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
```

**Solution:**
```java
public class Solution {
  public List<String[]> solveNQueens(int n) {
    List<String[]> res = new ArrayList<String[]>();
    helper(n, 0, new int[n], res);
    return res;
  }
    
  private void helper(int n, int row, int[] columnForRow, List<String[]> res) {
    if (row == n) {
      String[] sol = new String[n];
      for (int r = 0; r < n; r++) {
        sol[r] = "";
        for (int c = 0; c < n; c++) {
          sol[r] += (columnForRow[r] == c) ? "Q" : ".";
        }
      }
      res.add(sol);
      return;
    }
      
    for (int col = 0; col < n; col++) {
      columnForRow[row] = col;
        
      if (check(row, col, columnForRow)) {
        helper(n, row + 1, columnForRow, res);
      }
    }
  }
    
  private boolean check(int row, int col, int[] columnForRow) {
    for (int r = 0; r < row; r++) {
      if (columnForRow[r] == col || row - r == Math.abs(columnForRow[r] - col)) {
        return false;
      }
    }
    return true;
  }
}
```