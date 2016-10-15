# Closest Binary Search Tree Value

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

* Given target value is a floating point.
* You are guaranteed to have only one unique value in the BST that is closest to the target.

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
  public int closestValue(TreeNode root, double target) {
    int closest = root.val;

    while (root != null) {
      if (Math.abs(root.val - target) < Math.abs(closest - target)) {
        closest = root.val;
      }

      if (target < root.val) {
        root = root.left;
      } else {
        root = root.right;
      }
    }

    return closest;
  }
}
```