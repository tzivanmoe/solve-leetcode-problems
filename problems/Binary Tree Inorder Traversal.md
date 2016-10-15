# Binary Tree Inorder Traversal

Given a binary tree, return the inorder traversal of its nodes' values.

For example:

Given binary tree `[1,null,2,3]`,
```
   1
    \
     2
    /
   3
```

return `[1,3,2]`.

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
  public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();

    TreeNode curr = root;
    Stack<TreeNode> stack = new Stack<>();

    while (!stack.isEmpty() || curr != null) {
      if (curr != null) {
        stack.push(curr);
        curr = curr.left;
      } else {
        curr = stack.pop();
        list.add(curr.val);
        curr = curr.right;
      }
    }

    return list;
  }
}
```