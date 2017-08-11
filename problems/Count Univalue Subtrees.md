# Count Univalue Subtrees

Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

For example:

Given binary tree,
```
              5
             / \
            1   5
           / \   \
          5   5   5
```
return `4`.

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
  int count;

  public int countUnivalSubtrees(TreeNode root) {
    count = 0;
    helper(root);
    return count;
  }

  boolean helper(TreeNode root) {
    if (root == null)
      return true;

    boolean left = helper(root.left);
    boolean right = helper(root.right);

    if (left && right && (root.left == null || root.val == root.left.val) && (root.right == null || root.val == root.right.val)) {
      count++;
      return true;
    }

    return false;
  }
}
```

# Check Univalue Tree

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
  public boolean isUnivalTree(TreeNode root) {
    if (root == null)
      return false;
    
    return helper(root, root.val);
  }
  
  boolean helper(TreeNode root, in val) {
    if (root == null)
      return true;
      
    if (root.val != val)
      return false;
      
    return helper(root.left, val) && helper(root.right, val);
  }
}
```
