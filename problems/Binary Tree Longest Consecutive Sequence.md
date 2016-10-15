# Binary Tree Longest Consecutive Sequence

Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

For example,
```
   1
    \
     3
    / \
   2   4
        \
         5
```

Longest consecutive sequence path is `3-4-5`, so return `3`.

````
   2
    \
     3
    / 
   2    
  / 
 1
```

Longest consecutive sequence path is `2-3`,not `3-2-1`, so return `2`.

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
  int max;

  public int longestConsecutive(TreeNode root) {
    max = 0;
    helper(root);
    return max;
  }

  int helper(TreeNode root) {
    if (root == null) return 0;

    int len = 1;
    int left = helper(root.left);
    int right = helper(root.right);

    if (root.left != null && root.val == root.left.val - 1) {
      len = Math.max(len, left + 1);
    }

    if (root.right != null && root.val == root.right.val - 1) {
      len = Math.max(len, right + 1);
    }

    max = Math.max(len, max);

    return len;
  }
}
```