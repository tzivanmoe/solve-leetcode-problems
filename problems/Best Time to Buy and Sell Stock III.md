# Best Time to Buy and Sell Stock III

Say you have an array for which the *i*-th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

**Note:**

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**Solution:**
```java
public class Solution {
  public int maxProfit(int[] prices) {
    if (prices == null || prices.length == 0) { 
      return 0;
    }
        
    int n = prices.length;
    int profit = 0;
        
    // scan from left
    // left[i] keeps the max profit from 0 to i
    int[] left = new int[n];
    int min = prices[0];
        
    for (int i = 1; i < n; i++) {
      left[i] = Math.max(left[i - 1], prices[i] - min);
      min = Math.min(min, prices[i]);
    }
        
    // scan from right
    // right[i] keeps the max profit from i to n - 1
    int[] right = new int[n];
    int max = prices[n - 1];
        
    for (int i = n - 2; i >= 0; i--) {
      right[i] = Math.max(right[i + 1], max - prices[i]);
      max = Math.max(max, prices[i]);
            
      profit = Math.max(profit, left[i] + right[i]);
    }
        
    return profit;
  }
}
```

Time complexity: O(n)