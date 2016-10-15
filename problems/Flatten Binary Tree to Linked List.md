# Flatten Binary Tree to Linked List

Given a binary tree, flatten it to a linked list in-place.

For example,

Given
```
         1
        / \
       2   5
      / \   \
     3   4   6
```
The flattened tree should look like:
```
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
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
  public void flatten(TreeNode root) {
    if (root == null)
      return;

    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);

    TreeNode last = null;

    while (!stack.isEmpty()) {
      TreeNode curr = stack.pop();

      if (last != null) {
        last.left = null;
        last.right = curr;
      }

      if (curr.right != null)
        stack.push(curr.right);

      if (curr.left != null)
        stack.push(curr.left);

      last = curr;
    }
  }
}
```
