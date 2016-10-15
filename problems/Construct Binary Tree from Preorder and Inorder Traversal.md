# Construct Binary Tree from Preorder and Inorder Traversal

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**

You may assume that duplicates do not exist in the tree.

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
  public TreeNode buildTree(int[] preorder, int[] inorder) {
    Map<Integer, Integer> map = new HashMap<>();
        
    for (int i = 0; i < inorder.length; i++) {
      map.put(inorder[i], i);
    }
        
    return build(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1, map);
  }
    
  TreeNode build(int[] pre, int i1, int j1, int[] in, int i2, int j2, Map<Integer, Integer> map) {
    if (i1 > j1 || i2 > j2) {
      return null;
    }
            
    TreeNode root = new TreeNode(pre[i1]);
        
    int index = map.get(root.val);
    int nleft = index - i2;
        
    root.left = build(pre, i1 + 1, i1 + nleft, in, i2, index - 1, map);
    root.right = build(pre, i1 + nleft + 1, j1, in, index + 1, j2, map);
        
    return root;
  }
}
```