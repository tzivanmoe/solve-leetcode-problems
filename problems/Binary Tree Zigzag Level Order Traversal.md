# Binary Tree Zigzag Level Order Traversal

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:

Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
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
  public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();

    if (root == null) {
      return res;
    }

    List<Integer> list = new ArrayList<>();

    Stack<TreeNode> s1 = new Stack<>();
    Stack<TreeNode> s2 = new Stack<>();

    boolean leftToRight = true;

    s1.push(root);

    while (!s1.isEmpty()) {
      TreeNode node = s1.pop();

      list.add(node.val);

      if (leftToRight) {
        if (node.left != null) {
          s2.push(node.left);
        }

        if (node.right != null) {
          s2.push(node.right);
        }
      } else {
        if (node.right != null) {
          s2.push(node.right);
        }

        if (node.left != null) {
          s2.push(node.left);
        }
      }

      if (s1.isEmpty()) {
        leftToRight = !leftToRight;
        res.add(new ArrayList<>(list));
        list = new ArrayList<>();

        s1 = s2;
        s2 = new Stack<>();
      }
    }

    return res;
  }
}
```