# Summary Ranges

Given a sorted integer array without duplicates, return the summary of its ranges.

For example, given `[0,1,2,4,5,7]`, return `["0->2","4->5","7"]`.

**Solution:**
```java
public class Solution {
  public List<String> summaryRanges(int[] a) {
    List<String> res = new ArrayList<String>();
        
    if (a == null) 
      return res;
            
    int i = 0, n = a.length;
        
    for (int j = 1; j < n; j++) {
      if ((long)a[j] - (long)a[j - 1] > 1) {
        // found a range
        res.add(getRange(a[i], a[j - 1]));
        i = j;
      }
    }
        
    // do a final check
    if (i < n) 
      res.add(getRange(a[i], a[n - 1]));
        
    return res;
  }
    
  String getRange(int n1, int n2) {
    return (n1 == n2) ? String.valueOf(n1) : String.format("%d->%d", n1, n2);
  }
}
```