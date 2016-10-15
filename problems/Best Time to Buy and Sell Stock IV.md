# Best Time to Buy and Sell Stock IV

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most k transactions.

**Note:**

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**Solution:**
```java
public class Solution {
  public int maxProfit(int k, int[] prices) {
    int n = prices.length;

    if (k >= n) {
        return solveMaxProfit(prices);
    }

    // The local array tracks maximum profit of j transactions & the last transaction is on ith day. 
    // The global array tracks the maximum profit of j transactions until ith day.
    int[][] local = new int[n][k + 1];
    int[][] global = new int[n][k + 1];

    for (int i = 1; i < n; i++) {
      int diff = prices[i] - prices[i - 1];

      for (int j = 1; j <= k; j++) {
        local[i][j] = Math.max(
          global[i - 1][j - 1] + Math.max(diff, 0),
          local[i - 1][j] + diff
        );

        global[i][j] = Math.max(global[i - 1][j], local[i][j]);
      }
    }

    return global[n - 1][k];
  }

  private int solveMaxProfit(int[] prices) {
    int profit = 0;

    for (int i = 1; i < prices.length; i++) {
      // as long as there is a price gap, we gain a profit.
      if (prices[i] > prices[i - 1]) {
        profit += prices[i] - prices[i - 1];
      }
    }

    return profit;
  }
}
```