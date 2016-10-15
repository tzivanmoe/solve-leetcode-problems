# Binary Tree Paths

Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:
```
   1
 /   \
2     3
 \
  5
```
All root-to-leaf paths are:
```
["1->2->5", "1->3"]
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
  public List<String> binaryTreePaths(TreeNode root) {
    List<String> res = new ArrayList<String>();
    helper(root, new ArrayList<Integer>(), res);
    return res;
  }

  void helper(TreeNode root, List<Integer> sol, List<String> res) {
    if (root == null) return;

    sol.add(root.val);

    if (root.left == null && root.right == null) {
      res.add(convert(sol));
    } else {
      helper(root.left, sol, res);
      helper(root.right, sol, res);
    }

    sol.remove(sol.size() - 1);
  }

  String convert(List<Integer> list) {
    StringBuilder sb = new StringBuilder();

    for (int i = 0; i < list.size(); i++) {
      if (i > 0) sb.append("->");
      sb.append(list.get(i));
    }

    return sb.toString();
  }
}
```