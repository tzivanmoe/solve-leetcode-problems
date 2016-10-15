# Binary Tree Right Side View

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:

Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
You should return `[1, 3, 4]`.

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
  public List<Integer> rightSideView(TreeNode root) {
    List<Integer> res = new ArrayList<Integer>();

    if (root == null)
      return res;

    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.add(root);
    queue.add(null);

    List<Integer> list = new ArrayList<Integer>();

    while (!queue.isEmpty()) {
      TreeNode node = queue.poll();

      if (node != null) {
        list.add(node.val);

        if (node.left != null)
          queue.add(node.left);

        if (node.right != null)
          queue.add(node.right);
      } else {
        res.add(list.get(list.size() - 1));

        if (!queue.isEmpty())
          queue.add(null);
      }
    }

    return res;
  }
}
```