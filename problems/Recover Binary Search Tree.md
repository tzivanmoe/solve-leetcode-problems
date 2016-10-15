# Recover Binary Search Tree

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

**Note:**

A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

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
  public void recoverTree(TreeNode root) {
    if (root == null)
      return;

    TreeNode a = null;
    TreeNode b = null;

    TreeNode prev = null;
    TreeNode curr = root;
    Stack<TreeNode> stack = new Stack<>();

    while (!stack.isEmpty() || curr != null) {
      if (curr != null) {
        stack.push(curr);
        curr = curr.left;
      } else {
        curr = stack.pop();

        if (prev != null && prev.val > curr.val) {
          if (a == null) {
            a = prev;
          }

          b = curr;
        }

        prev = curr;
        curr = curr.right;
      }
    }

    // swap a and b to fix the problem
    if (a != null && b != null) {
      int tmp = a.val;
      a.val = b.val;
      b.val = tmp;
    }
  }
}
```