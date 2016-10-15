# Path Sum II

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:

Given the below binary tree and `sum = 22`,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
return
```
[
   [5,4,11,2],
   [5,8,4,5]
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
  public List<List<Integer>> pathSum(TreeNode root, int sum) {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> sol = new ArrayList<>();

    helper(root, sum, sol, res);

    return res;
  }

  void helper(TreeNode root, int sum, List<Integer> sol, List<List<Integer>> res) {
    if (root == null)
      return;

    sol.add(root.val);

    if (root.left == null && root.right == null && root.val == sum) {
      res.add(new ArrayList<>(sol));
    } else {
      helper(root.left, sum - root.val, sol, res);
      helper(root.right, sum - root.val, sol, res);
    }

    sol.remove(sol.size() - 1);
  }
}
```