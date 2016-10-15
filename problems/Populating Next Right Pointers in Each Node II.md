# Populating Next Right Pointers in Each Node II

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

**Note:**

* You may only use constant extra space.

For example,

Given the following binary tree,
```
         1
       /  \
      2    3
     / \    \
    4   5    7
```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```

**Solution:**
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
  public void connect(TreeLinkNode root) {
    while (root != null) {
      TreeLinkNode curr = root;

      while (curr != null) {
        if (curr.left != null) {
          if (curr.right != null) {
            curr.left.next = curr.right;
          } else {
            curr.left.next = getNext(curr.next);
          }
        }

        if (curr.right != null) {
          curr.right.next = getNext(curr.next);
        }

        curr = curr.next;
      }

      root = getNext(root);
    }
  }

  TreeLinkNode getNext(TreeLinkNode node) {
    while (node != null) {
      if (node.left != null)
        return node.left;

      if (node.right != null)
        return node.right;

      node = node.next;
    }

    return null;
  }
}
```