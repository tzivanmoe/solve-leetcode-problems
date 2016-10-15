# Meeting Rooms II

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...]` (si < ei), find the minimum number of conference rooms required.

For example,

Given `[[0, 30],[5, 10],[15, 20]]`,

return `2`.

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
  public int minMeetingRooms(Interval[] intervals) {
    if (intervals == null || intervals.length == 0)
      return 0;

    // Sort the intervals by start time
    Arrays.sort(intervals, new Comparator<Interval>() {
      public int compare(Interval a, Interval b) { return a.start - b.start; }
    });

    // Use a min heap to track the minimum end time of merged intervals
    PriorityQueue<Interval> heap = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>() {
      public int compare(Interval a, Interval b) { return a.end - b.end; }
    });

    heap.offer(intervals[0]);

    for (int i = 1; i < intervals.length; i++) {
      Interval interval = heap.poll();

      if (intervals[i].start >= interval.end) {
        interval.end = intervals[i].end;
      } else {
        heap.offer(intervals[i]);
      }

      heap.offer(interval);
    }

    return heap.size();
  }
}
```