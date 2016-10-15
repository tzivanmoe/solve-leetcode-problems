# Binary Tree Level Order Traversal II

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

**For example:**

Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its bottom-up level order traversal as:
```
[
  [15,7],
  [9,20],
  [3]
]
```

**Solution:**
```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
  public List<List<Integer>> levelOrderBottom(TreeNode root) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    List<Integer> list = new ArrayList<Integer>();

    if (root == null) {
      return res;
    }

    Queue<TreeNode> curr = new LinkedList<TreeNode>();
    Queue<TreeNode> next = new LinkedList<TreeNode>();

    curr.add(root);

    while (!curr.isEmpty()) {
      TreeNode node = curr.poll();
      list.add(node.val);

      if (node.left != null) {
        next.add(node.left);
      }

      if (node.right != null) {
        next.add(node.right);
      }

      if (curr.isEmpty()) {
        res.add(0, list);
        list = new ArrayList<Integer>();

        curr = next;
        next = new LinkedList<TreeNode>();
      }
    }

    return res;
  }
}
```