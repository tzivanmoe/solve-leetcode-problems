# Convert Sorted Array to Binary Search Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

**Solution:**
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
  public TreeNode sortedArrayToBST(int[] nums) {
    return build(nums, 0, nums.length - 1);
  }

  TreeNode build(int[] nums, int lo, int hi) {
    if (lo > hi)
      return null;

    int mid = lo + (hi - lo) / 2;

    TreeNode root = new TreeNode(nums[mid]);

    root.left = build(nums, lo, mid - 1);
    root.right = build(nums, mid + 1, hi);

    return root;
  }
}
```