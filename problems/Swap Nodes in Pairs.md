# Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

For example,

Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

**Solution:**
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
  public ListNode swapPairs(ListNode head) {
    // Base Case: The list is empty or has only one node
    if (head == null || head.next == null)
      return head;

    // Store head of list after two nodes
    ListNode rest = head.next.next;

    // Change head
    ListNode newhead = head.next;

    // Change next of second node
    head.next.next = head;

    // Recur for remaining list and change next of head
    head.next = swapPairs(rest);

    // Return new head of modified list
    return newhead;
  }
}
```