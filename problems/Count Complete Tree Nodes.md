# Count Complete Tree Nodes

Given a complete binary tree, count the number of nodes.

Definition of a complete binary tree from Wikipedia:

In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

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
  public int countNodes(TreeNode root) {
    if (root == null)
      return 0;

    int hLeft = getHeight(root.left);
    int hRight = getHeight(root.right);

    if (hLeft == hRight)
      return (1 << hLeft) + countNodes(root.right);
    else
      return (1 << hRight) + countNodes(root.left);
  }

  int getHeight(TreeNode root) {
    if (root == null)
      return 0;

    return 1 + getHeight(root.left);
  }
}
```