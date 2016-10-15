# Trapping Rain Water

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example, 

Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return 6.

![](rainwatertrap.png)

The above elevation map is represented by array `[0,1,0,2,1,0,1,3,2,1,2,1]`. In this case, 6 units of rain water (blue section) are being trapped.

**Solution:**
```java
public class Solution {
  public int trap(int[] height) {
    if (height == null || height.length == 0) {
      return 0;
    }
        
    int n = height.length;
    int max = 0;
        
    // scan from left
    int[] lmax = new int[n];
    for (int i = 0; i < n; i++) {
      lmax[i] = max;
      max = Math.max(max, height[i]);
    }
        
    // scan from right
    max = 0;
    int[] rmax = new int[n];
    for (int i = n - 1; i >= 0; i--) {
      rmax[i] = max;
      max = Math.max(max, height[i]);
    }
        
    // final scan
    int res = 0;
    for (int i = 0; i < n; i++) {
      int water = Math.min(lmax[i], rmax[i]) - height[i];
      res += water >= 0 ? water : 0;
    }
        
    return res;
  }
}
```