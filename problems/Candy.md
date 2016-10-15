# Candy

There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

* Each child must have at least one candy.
* Children with a higher rating get more candies than their neighbors.


What is the minimum candies you must give?

**Solution:**
```java
public class Solution {
  public int candy(int[] ratings) {
    if (ratings == null || ratings.length == 0) return 0;

    int n = ratings.length;

    // arr[i] stores the num of candies of i-th kid
    int[] arr = new int[n]; arr[0] = 1;

    // scan from left to right
    for (int i = 1; i < n; i++)
      arr[i] = (ratings[i] > ratings[i - 1]) ? arr[i - 1] + 1 : 1;

    // scan from right to left
    int sum = arr[n - 1];

    for (int i = n - 2; i >= 0; i--) {
      if (ratings[i] > ratings[i + 1])
        arr[i] = Math.max(arr[i], arr[i + 1] + 1);

      sum += arr[i];
    }

    return sum;
  }
}
```