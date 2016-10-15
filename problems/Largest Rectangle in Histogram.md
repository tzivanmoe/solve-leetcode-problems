# Largest Rectangle in Histogram

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](histogram.png)

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![](histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = `10` unit.

**For example,**

Given heights = `[2,1,5,6,2,3]`,
return `10`.

**Solution:**
```java
public class Solution {
  public int largestRectangleArea(int[] h) {
    int n = h.length, i = 0, max = 0;
        
    Stack<Integer> s = new Stack<>();
        
    while (i < n) {
      while (!s.isEmpty() && h[i] < h[s.peek()]) {
        max = Math.max(max, h[s.pop()] * (i - (s.isEmpty() ? 0 : s.peek() + 1)));
      }
      s.push(i++);
    }
        
    while (!s.isEmpty()) {
      max = Math.max(max, h[s.pop()] * (n - (s.isEmpty() ? 0 : s.peek() + 1)));
    }
        
    return max;
  }
}
```