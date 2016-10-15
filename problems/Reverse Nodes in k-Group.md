# Reverse Nodes in k-Group

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

For example,

Given this linked list: `1->2->3->4->5`

For k = 2, you should return: `2->1->4->3->5`

For k = 3, you should return: `3->2->1->4->5`

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
public class Solution {
  public ListNode reverseKGroup(ListNode head, int k) {
    if (getLength(head) < k) {
      return head;
    }

    ListNode prev = null;
    ListNode curr = head;

    int count = k;
    while (curr != null && count > 0) {
      ListNode next = curr.next;
      curr.next = prev;
      prev = curr;
      curr = next;
      count--;
    }

    // prev is the new head
    // head is the new tail
    // curr is the next list

    head.next = reverseKGroup(curr, k);

    return prev;
  }

  int getLength(ListNode head) {
      int len = 0;

      while (head != null) {
          head = head.next;
          len++;
      }

      return len;
  }
}
```