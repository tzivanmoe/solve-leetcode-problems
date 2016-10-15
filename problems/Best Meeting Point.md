# Best Meeting Point

A group of two or more people wants to meet and minimize the total travel distance. You are given a 2D grid of values 0 or 1, where each 1 marks the home of someone in the group. The distance is calculated using Manhattan Distance, where `distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|`.

For example, given three people living at `(0,0)`, `(0,4)`, and `(2,2)`:

```
1 - 0 - 0 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0
```

The point `(0,2)` is an ideal meeting point, as the total travel distance of `2+2+2=6` is minimal. So return `6`.

**Hint:**

Try to solve it in one dimension first. How can this solution apply to the two dimension case?

**Solution:**
```java
import java.util.Random;

public class Solution {
  public int minTotalDistance(int[][] grid) {
    List<Integer> x = new ArrayList<>();
    List<Integer> y = new ArrayList<>();

    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == 1) {
          x.add(i); y.add(j);
        }
      }
    }

    // get median of x[] and y[] using quick select
    int mx = x.get(quickSelect(x, 0, x.size() - 1, x.size() / 2 + 1));
    int my = y.get(quickSelect(y, 0, y.size() - 1, y.size() / 2 + 1));

    // calculate the total Manhattan distance
    int total = 0;
    for (int i = 0; i < x.size(); i++) {
      total += Math.abs(x.get(i) - mx) + Math.abs(y.get(i) - my);
    }
    return total;
  }

  // return the index of the kth smallest number
  // avg. O(n) time complexity
  int quickSelect(List<Integer> a, int lo, int hi, int k) {
    // use quick sort's idea
    // randomly pick a pivot and put it to a[hi]
    // we need to do this, otherwise quick sort is slow!
    Random rand = new Random();
    int p = lo + rand.nextInt(hi - lo + 1);
    Collections.swap(a, p, hi);

    // put nums that are <= pivot to the left
    // put nums that are  > pivot to the right
    int i = lo, j = hi, pivot = a.get(hi);
    while (i < j) {
      if (a.get(i++) > pivot) Collections.swap(a, --i, --j);
    }
    Collections.swap(a, i, hi);

    // count the nums that are <= pivot from lo
    int m = i - lo + 1;

    // pivot is the one!
    if (m == k)     return i;
    // pivot is too big, so it must be on the left
    else if (m > k) return quickSelect(a, lo, i - 1, k);
    // pivot is too small, so it must be on the right
    else            return quickSelect(a, i + 1, hi, k - m);
  }
}
```
