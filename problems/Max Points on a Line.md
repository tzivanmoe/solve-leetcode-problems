# Max Points on a Line

Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

**Solution:**
```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
public class Solution {
  public int maxPoints(Point[] points) {
    if (points == null || points.length == 0)
      return 0;

    int n = points.length, max = 1;

    Map<String, Set<Point>> map = new HashMap<String, Set<Point>>();

    // sort the points by x to avoid -0.0 issue!
    Collections.sort(Arrays.asList(points), new Comparator<Point>() {
        public int compare(Point a, Point b) { return a.x - b.x; }
    });

    for (int i = 0; i < n; i++) {
      for (int j = i + 1; j < n; j++) {
        Point p1 = points[i];
        Point p2 = points[j];

        StringBuilder sb = new StringBuilder();

        if (p1.x == p2.x) {
          sb.append("inf").append(p1.x);
        } else {
          // y = k * x + d
          double k = (double)(p1.y - p2.y) / (p1.x - p2.x);
          double d = p1.y - k * p1.x;
          sb.append("k").append(k).append("d").append(d);
        }

        String key = sb.toString();
        Set<Point> set = map.containsKey(key) ? map.get(key) : new HashSet<Point>();

        set.add(p1);
        set.add(p2);

        map.put(key, set);
        max = Math.max(max, set.size());
      }
    }

    return max;
  }
}
```