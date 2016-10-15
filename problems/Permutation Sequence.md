# Permutation Sequence

The set `[1,2,3,...,n]` contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`
7. 
Given n and k, return the k-th permutation sequence.

**Note:** Given n will be between 1 and 9 inclusive.

**Solution:**
```java
public class Solution {
  public String getPermutation(int n, int k) {
    // step 1. prepare the number sequence
    List<Integer> nums = new ArrayList<Integer>();
    for (int i = 1; i <= n; i++) {
      nums.add(i);
    }
        
    // step 2. calculate (n-1)!
    int[] f = new int[n];
    f[0] = 1;
    for (int i = 1; i < n; i++) {
      f[i] = f[i - 1] * i; 
    }
        
    // step 3. calculate each digit, total n digits
    StringBuilder sb = new StringBuilder();
        
    k--;
    while (n > 0) {
      int p = k  / f[n - 1];
            
      sb.append(nums.get(p));
      nums.remove(p);
            
      k = k % f[n - 1];
            
      n--;
    }
        
    return sb.toString();
  }
}
```