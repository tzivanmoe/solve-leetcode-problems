# Find Median from Data Stream

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

**Examples: **

`[2,3,4]` , the median is `3`

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum(int num) - Add a integer number from the data stream to the data structure.
* double findMedian() - Return the median of all elements so far.

**For example:**

```
add(1)
add(2)
findMedian() -> 1.5
add(3) 
findMedian() -> 2
```

**Solution:**
```java
class MedianFinder {
  // Max heap
  PriorityQueue<Integer> left = new PriorityQueue<>(new Comparator<Integer>() {
    public int compare(Integer a, Integer b) { return b - a; }
  });

  // Min heap
  PriorityQueue<Integer> right = new PriorityQueue<>(new Comparator<Integer>() {
    public int compare(Integer a, Integer b) { return a - b; }
  });

  // Adds a number into the data structure.
  public void addNum(int num) {
    double m = findMedian();

    int diff = left.size() - right.size();

    // left and right are balanced
    if (diff == 0) {
      if (num < m) {
        left.offer(num);
      } else {
        right.offer(num);
      }
    }
    // left has more elements than right
    else if (diff > 0) {
      if (num < m) {
        if (left.size() > 0) right.offer(left.poll());
        left.offer(num);
      } else {
        right.offer(num);
      }
    }
    // right has more elements than left
    else {
      if (num < m) {
        left.offer(num);
      } else {
        if (right.size() > 0) left.offer(right.poll());
        right.offer(num);
      }
    }
  }

  // Returns the median of current data stream
  public double findMedian() {
    if (left.size() == 0 && right.size() == 0) {
      return 0.0;
    }

    int diff = left.size() - right.size();

    // left and right are balanced
    if (diff == 0) {
      return (left.peek() + right.peek()) / 2.0;
    }
    // left has more elements than right
    else if (diff > 0) {
      return left.peek();
    }
    // right has more elements than left
    else {
      return right.peek();
    }
  }
};

// Your MedianFinder object will be instantiated and called as such:
// MedianFinder mf = new MedianFinder();
// mf.addNum(1);
// mf.findMedian();
```