# Binary Tree Preorder Traversal

Given a binary tree, return the preorder traversal of its nodes' values.

For example:

Given binary tree `{1,#,2,3}`,
```
   1
    \
     2
    /
   3
```

return `[1,2,3]`.

**Note:** Recursive solution is trivial, could you do it iteratively?

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
  public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<Integer>();

    if (root == null)
      return res;

    Stack<TreeNode> stack = new Stack<TreeNode>();
    stack.push(root);

    while (!stack.isEmpty()) {
      TreeNode node = stack.pop();
      res.add(node.val);

      if (node.right != null)
        stack.push(node.right);

      if (node.left != null)
        stack.push(node.left);
    }

    return res;
  }
}
```