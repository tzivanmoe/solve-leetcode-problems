# Reverse Linked List II

Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:

Given `1->2->3->4->5->NULL`, m = 2 and n = 4,

return `1->4->3->2->5->NULL`.

**Note:**

Given m, n satisfy the following condition: 1 ≤ m ≤ n ≤ length of list.

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
  public ListNode reverseBetween(ListNode head, int m, int n) {
    if (head == null || head.next == null) {
        return head;
    }

    int k = n - m + 1;

    ListNode f = new ListNode(0);
    f.next = head;

    ListNode p = f;
    ListNode c = head;

    // locate the m-th node
    while (m > 1) {
      p = c;
      c = c.next;
      m--;
    }

    // reverse till n-th node
    ListNode prev = null;
    ListNode curr = c;
    ListNode next = null;

    while (k > 0) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
      curr = next;
      k--;
    }

    // re-link
    p.next = prev;
    c.next = curr;

    return f.next;
  }
}
```