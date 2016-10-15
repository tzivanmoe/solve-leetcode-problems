# Zigzag Iterator

Given two 1d vectors, implement an iterator to return their elements alternately.

For example, given two 1d vectors:

```
v1 = [1, 2]
v2 = [3, 4, 5, 6]
```

By calling next repeatedly until hasNext returns `false`, the order of elements returned by next should be: `[1, 3, 2, 4, 5, 6]`.

**Follow up:** What if you are given k 1d vectors? How well can your code be extended to such cases?

The "Zigzag" order is not clearly defined and is ambiguous for `k > 2` cases. If "Zigzag" does not look right to you, replace "Zigzag" with "Cyclic". For example, given the following input:

```
[1,2,3]
[4,5,6,7]
[8,9]
```

It should return `[1,4,8,2,5,9,3,6,7]`.

**Solution:**
```java
public class ZigzagIterator {
  int i1 = 0;
  int i2 = 0;

  boolean flag = false;

  List<Integer> l1;
  List<Integer> l2;

  public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
    l1 = v1;
    l2 = v2;
  }

  public int next() {
    flag = !flag;

    if (i1 < l1.size() && (flag  || i2 >= l2.size())) 
      return l1.get(i1++);

    if (i2 < l2.size() && (!flag || i1 >= l1.size())) 
      return l2.get(i2++);

    return -1;
  }

  public boolean hasNext() {
    return i1 < l1.size() || i2 < l2.size();
  }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```