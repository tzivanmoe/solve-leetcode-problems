# Median of Two Sorted Arrays

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

**Example 1:**
```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

**Solution:**
```java
public class Solution {
  public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int l1 = nums1.length;
    int l2 = nums2.length;
        
    int k = (l1 + l2) / 2;
        
    if ((l1 + l2) % 2 == 0) {
      return (helper(nums1, 0, l1 - 1, nums2, 0, l2 - 1, k) + helper(nums1, 0, l1 - 1, nums2, 0, l2 - 1, k + 1)) / 2.0;
    } else {
      return helper(nums1, 0, l1 - 1, nums2, 0, l2 - 1, k + 1);
    }
  }
    
  double helper(int[] a1, int i1, int j1, int[] a2, int i2, int j2, int k) {
    int l1 = j1 - i1 + 1;
    int l2 = j2 - i2 + 1;
        
    if (l1 > l2) {
      return helper(a2, i2, j2, a1, i1, j1, k);
    }
        
    if (l1 == 0) {
      return a2[i2 + k - 1];
    }
        
    if (k == 1) {
      return Math.min(a1[i1], a2[i2]);
    }
        
    int n1 = Math.min(k / 2, l1);
    int n2 = k - n1;
        
    int v1 = a1[i1 + n1 - 1];
    int v2 = a2[i2 + n2 - 1];
        
    if (v1 == v2) {
      return v1;
    } else if (v1 < v2) {
      return helper(a1, i1 + n1, j1, a2, i2, i2 + n2 - 1, k - n1);
    } else {
      return helper(a1, i1, i1 + n1 - 1, a2, i2 + n2, j2, k - n2);
    }
  }
}
```