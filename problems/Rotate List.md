# Rotate List

Given a list, rotate the list to the right by k places, where k is non-negative.

For example:

Given `1->2->3->4->5->NULL` and k = `2`,

return `4->5->1->2->3->NULL`.

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
  public ListNode rotateRight(ListNode head, int k) {
    if (head == null) {
      return null;
    }

    int len = getLength(head);
    k %= len;

    if (k == 0) {
      return head;
    }

    ListNode fast = head;
    ListNode slow = head;

    while (fast != null && k > 0) {
      fast = fast.next;
      k--;
    }

    while (fast.next != null) {
      slow = slow.next;
      fast = fast.next;
    }

    fast.next = head;
    head = slow.next;
    slow.next = null;

    return head;
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