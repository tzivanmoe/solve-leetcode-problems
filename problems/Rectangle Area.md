# Rectangle Area

Find the total area covered by two **rectilinear** rectangles in a **2D** plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

![](rectangle_area.png)

Assume that the total area is never beyond the maximum possible value of int.

**Solution:**
```java
public class Solution {
  public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
    long total = (C - A) * (D - B) + (G - E) * (H - F);

    long w = (long)Math.min(C, G) - (long)Math.max(A, E);
    long h = (long)Math.min(D, H) - (long)Math.max(B, F);

    long common = (w < 0 || h < 0) ? 0 : w * h;

    return (int)(total - common);
  }
}
```