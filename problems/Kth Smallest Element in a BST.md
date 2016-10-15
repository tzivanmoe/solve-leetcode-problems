# Kth Smallest Element in a BST

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Note:**

You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Follow up:**

What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

**Hint:**

1. Try to utilize the property of a BST.
2. What if you could modify the BST node's structure?
3. The optimal runtime complexity is O(height of BST).

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
  public int kthSmallest(TreeNode root, int k) {
    int nLeft = countNodes(root.left);

    if (nLeft == k - 1)
      return root.val;

    else if (nLeft > k - 1)
      return kthSmallest(root.left, k);

    else
      return kthSmallest(root.right, k - nLeft - 1);
  }

  int countNodes(TreeNode root) {
    if (root == null)
      return 0;

    return 1 + countNodes(root.left) + countNodes(root.right);
  }
}
```