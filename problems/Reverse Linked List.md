# Reverse Linked List

Reverse a singly linked list.

**Hint:**

A linked list can be reversed either iteratively or recursively. Could you implement both?

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
  public ListNode reverseList(ListNode head) {
    if (head == null)
      return null;

    ListNode prev = null, curr = head, next = null;

    while (curr != null) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
      curr = next;
    }

    return prev;
  }
}
```