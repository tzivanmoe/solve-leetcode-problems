# Merge Sorted Array

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

**Note:**

You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

**Solution:**
```java
public class Solution {
  public void merge(int[] nums1, int m, int[] nums2, int n) {
    int[] copy = new int[m];
        
    for (int k = 0; k < m; k++)
      copy[k] = nums1[k];
            
    int i = 0, j = 0;
        
    for (int k = 0; k < m + n; k++) {
      if (i >= m)                  nums1[k] = nums2[j++];
      else if (j >= n)             nums1[k] = copy[i++];
      else if (copy[i] < nums2[j]) nums1[k] = copy[i++];
      else                         nums1[k] = nums2[j++];
    }
  }
}
```