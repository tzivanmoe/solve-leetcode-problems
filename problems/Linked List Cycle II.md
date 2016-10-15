# Linked List Cycle II

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

Note: Do not modify the linked list.

Follow up:

Can you solve it without using extra space?

**Solution:**
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
  public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;

      if (slow == fast)
        break;
    }

    if (fast == null || fast.next == null)
      return null;

    slow = head;
    while (slow != fast) {
      slow = slow.next;
      fast = fast.next;
    }

    return slow;
  }
}
```