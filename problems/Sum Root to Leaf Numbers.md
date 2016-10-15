# Sum Root to Leaf Numbers

Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path `1->2->3` which represents the number `123``.

Find the total sum of all root-to-leaf numbers.

For example,
```
    1
   / \
  2   3
```
The root-to-leaf path `1->2` represents the number `12`.
The root-to-leaf path `1->3` represents the number `13`.

Return the sum = 12 + 13 = `25`.

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
  int total;

  public int sumNumbers(TreeNode root) {
    total = 0;
    helper(root, 0);
    return total;
  }

  void helper(TreeNode root, int sum) {
    if (root == null) return;

    sum = sum * 10 + root.val;

    if (root.left == null && root.right == null) {
      total += sum;
      return;
    }

    helper(root.left, sum);
    helper(root.right, sum);
  }
}
```