# Unique Binary Search Trees II

Given an integer n, generate all structurally unique **BST**'s (binary search trees) that store values 1...n.

For example,

Given n = 3, your program should return all 5 unique BST's shown below.
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

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
  public List<TreeNode> generateTrees(int n) {
      return helper(1, n);
  }

  List<TreeNode> helper(int lo, int hi) {
    List<TreeNode> res = new ArrayList<>();

    if (lo > hi) {
      res.add(null);
      return res;
    }

    if (lo == hi) {
      res.add(new TreeNode(lo));
      return res;
    }

    for (int i = lo; i <= hi; i++) {
      List<TreeNode> left = helper(lo, i - 1);
      List<TreeNode> right = helper(i + 1, hi);

      for (TreeNode l : left) {
        for (TreeNode r : right) {
          TreeNode root = new TreeNode(i);
          root.left = l;
          root.right = r;
          res.add(root);
        }
      }
    }

    return res;
  }
}
```