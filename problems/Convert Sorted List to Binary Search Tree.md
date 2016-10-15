# Convert Sorted List to Binary Search Tree

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

**Solution:**
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
  public TreeNode sortedListToBST(ListNode head) {
    if (head == null) {
      return null;
    }

    if (head.next == null) {
      TreeNode root = new TreeNode(head.val);
      return root;
    }

    // find middle node
    ListNode prev = null;
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next.next;
    }

    // slow is the middle node
    TreeNode root = new TreeNode(slow.val);

    prev.next = null;

    root.left = sortedListToBST(head);
    root.right = sortedListToBST(slow.next);

    return root;
  }
}
```