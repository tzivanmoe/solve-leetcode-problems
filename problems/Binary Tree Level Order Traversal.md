# Binary Tree Level Order Traversal

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

**For example:**

Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
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
  public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();

    if (root == null) {
      return res;
    }

    // Use a queue to help level order traversal
    Queue<TreeNode> queue = new LinkedList<TreeNode>();

    queue.offer(root);
    queue.offer(null);

    List<Integer> list = new ArrayList<Integer>();

    while (!queue.isEmpty()) {
      TreeNode node = queue.poll();

      if (node != null) {
        list.add(node.val);

        if (node.left != null) {
          queue.offer(node.left);
        }

        if (node.right != null) {
          queue.offer(node.right);
        }
      } else {
        res.add(new ArrayList<Integer>(list));
        list = new ArrayList<Integer>();

        if (!queue.isEmpty()) {
          queue.offer(null);
        }
      }
    }

    return res;
  }
}
```