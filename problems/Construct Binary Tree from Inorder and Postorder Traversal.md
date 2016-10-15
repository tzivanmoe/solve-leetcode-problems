# Construct Binary Tree from Inorder and Postorder Traversal

Given inorder and postorder traversal of a tree, construct the binary tree.

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
  public TreeNode buildTree(int[] inorder, int[] postorder) {
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        
    for (int i = 0; i < inorder.length; i++) {
      map.put(inorder[i], i);
    }
        
    return build(postorder, 0, postorder.length - 1, inorder, 0, inorder.length - 1, map);
  }
    
  TreeNode build(int[] post, int i1, int j1, int[] in, int i2, int j2, Map<Integer, Integer> map) {
    if (i1 > j1 || i2 > j2) {
      return null;
    }
            
    TreeNode root = new TreeNode(post[j1]);
        
    int index = map.get(root.val);
    int left = index - i2;
        
    root.left = build(post, i1, i1 + left - 1, in, i2, index - 1, map);
    root.right = build(post, i1 + left, j1 - 1, in, index + 1, j2, map);
        
    return root;
  }
}
```