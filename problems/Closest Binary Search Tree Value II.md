# Closest Binary Search Tree Value II

Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

**Note:**

* Given target value is a floating point.
* You may assume k is always valid, that is: k ≤ total nodes.
* You are guaranteed to have only one unique set of k values in the BST that are closest to the target.


**Follow up:**

Assume that the BST is balanced, could you solve it in less than O(n) runtime (where n = total nodes)?

**Hint:**

* Consider implement these two helper functions:
  1. getPredecessor(N), which returns the next smaller node to N.
  2. getSuccessor(N), which returns the next larger node to N.
* Try to assume that each node has a parent pointer, it makes the problem much easier.
* Without parent pointer we just need to keep track of the path from the root to the current node using a stack.
* You would need two stacks to track the path in finding predecessor and successor node separately.

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
  public List<Integer> closestKValues(TreeNode root, double target, int k) {
    List<Integer> res = new ArrayList<>();
    Stack<Integer> s1 = inorder(root, target, true);  // predecessors
    Stack<Integer> s2 = inorder(root, target, false); // successors

    while (k-- > 0) {
      if (s1.isEmpty())
        res.add(s2.pop());
      else if (s2.isEmpty())
        res.add(s1.pop());
      else if (Math.abs(s1.peek() - target) < Math.abs(s2.peek() - target))
        res.add(s1.pop());
      else
        res.add(s2.pop());
    }

    return res;
  }

  // iterative inorder traversal
  Stack<Integer> inorder(TreeNode root, double target, boolean reverse) {
    Stack<Integer> res = new Stack<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode curr = root;

    while (!stack.isEmpty() || curr != null) {
      if (curr != null) {
        stack.push(curr);
        curr = reverse ? curr.right : curr.left;
      } else {
        curr = stack.pop();
        if (reverse && curr.val <= target) break;
        if (!reverse && curr.val > target) break;
        res.push(curr.val);
        curr = reverse ? curr.left : curr.right;
      }
    }
    return res;
  }
}
```