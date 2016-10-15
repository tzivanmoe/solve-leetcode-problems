# Serialize and Deserialize Binary Tree

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree

```
    1
   / \
  2   3
     / \
    4   5
```

as `"[1,2,3,null,null,4,5]"`, just the same as how LeetCode OJ serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

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
public class Codec {

  // Encodes a tree to a single string.
  public String serialize(TreeNode root) {
    if (root == null) return null;

    String delim = "";
    StringBuilder sb = new StringBuilder();

    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);

    // preorder traversal
    while (!stack.isEmpty()) {
      TreeNode node = stack.pop();
      sb.append(delim).append(node == null ? "#" : String.valueOf(node.val));
      delim = ",";

      if (node != null) {
        stack.push(node.right);
        stack.push(node.left);
      }
    }

    return sb.toString();
  }

  // Decodes your encoded data to tree.
  public TreeNode deserialize(String data) {
    if (data == null) return null;

    String[] list = data.split(",");

    // create the root node and push it to the stack
    TreeNode root = new TreeNode(Integer.valueOf(list[0]));
    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);

    // direction flag
    boolean left = true;

    for (int i = 1; i < list.length; i++) {
      TreeNode node = list[i].equals("#") ? null : new TreeNode(Integer.valueOf(list[i]));

      if (left) {
        stack.peek().left = node;
        if (node == null) left = false;
      } else {
        stack.pop().right = node;
        if (node != null) left = true;
      }

      if (node != null) stack.push(node);
    }

    return root;
  }

}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```