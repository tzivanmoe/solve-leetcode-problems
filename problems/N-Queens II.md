# N-Queens II

Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.

![](8-queens.png)

**Solution:**
```java
public class Solution {
  int count;
    
  public int totalNQueens(int n) {
    count = 0;  
    helper(n, 0, new int[n]);
    return count;
  }
    
  private void helper(int n, int row, int[] columnForRow) {
    if (row == n) {
      count++;
      return;
    }
      
    for (int col = 0; col < n; col++) {
      columnForRow[row] = col;
      if (check(row, col, columnForRow)) {
        helper(n, row + 1, columnForRow);
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