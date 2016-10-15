# Binary Tree Postorder Traversal

Given a binary tree, return the postorder traversal of its nodes' values.

For example:

Given binary tree `{1,#,2,3}`,
```
   1
    \
     2
    /
   3
```
return `[3,2,1]`.

Note: Recursive solution is trivial, could you do it iteratively?

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
  public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<Integer>();

    if (root == null)
      return res;

    Stack<TreeNode> s1 = new Stack<TreeNode>();
    Stack<TreeNode> s2 = new Stack<TreeNode>();

    s1.push(root);

    while (!s1.isEmpty()) {
      TreeNode node = s1.pop();
      s2.push(node);

      if (node.left != null)
        s1.push(node.left);

      if (node.right != null)
        s1.push(node.right);
    }

    while (!s2.isEmpty())
      res.add(s2.pop().val);

    return res;
  }
}
```