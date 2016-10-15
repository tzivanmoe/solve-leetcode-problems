# Merge Intervals

Given a collection of intervals, merge all overlapping intervals.

For example,

Given `[1,3],[2,6],[8,10],[15,18]`,
return `[1,6],[8,10],[15,18]`.

**Solution:**
```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
  public List<Interval> merge(List<Interval> intervals) {
    // sort
    Collections.sort(intervals, new Comparator<Interval>() {
      public int compare(Interval a, Interval b) {
        return a.start - b.start;
      }
    });
        
    // merge
    Stack<Interval> stack = new Stack<Interval>();
        
    for (int i = 0; i < intervals.size(); i++) {
      Interval curr = intervals.get(i);
            
      if (stack.isEmpty() || curr.start > stack.peek().end) {
        stack.push(curr);
      } else {
        stack.peek().end = Math.max(curr.end, stack.peek().end);
      }
    }
        
    // return
    List<Interval> res = new ArrayList<Interval>();
    while (!stack.isEmpty()) {
      res.add(stack.pop());
    }
        
    return res;
  }
}
```