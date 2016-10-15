# Majority Element II

Given an integer array of size n, find all elements that appear more than `⌊ n/3 ⌋` times. The algorithm should run in linear time and in O(1) space.

**Solution:**
```java
public class Solution {
  public List<Integer> majorityElement(int[] a) {
    // we can only have maximum 2 majority elements
    int n = a.length;
    int c1 = 0, c2 = 0;
    Integer m1 = null, m2 = null;
        
    // step 1. find out those 2 majority elements
    // using Moore majority voting algorithm
    for (int i = 0; i < n; i++) {
      if (m1 != null && a[i] == m1) {
        c1++;
      } else if (m2 != null && a[i] == m2) {
        c2++;
      } else if (c1 == 0) {
        m1 = a[i]; c1 = 1;
      } else if (c2 == 0) {
        m2 = a[i]; c2 = 1;
      } else {
        c1--; c2--;
      }
    }
        
    // step 2. double check
    c1 = 0; c2 = 0;
        
    for (int i = 0; i < n; i++) {
      if (m1 != null && a[i] == m1) c1++;
      if (m2 != null && a[i] == m2) c2++;
    }
        
    List<Integer> res = new ArrayList<Integer>();
        
    if (c1 > n / 3) res.add(m1);
    if (c2 > n / 3) res.add(m2);
        
    return res;
  }
}
```