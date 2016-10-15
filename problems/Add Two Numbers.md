# Add Two Numbers

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input:** (2 -> 4 -> 3) + (5 -> 6 -> 4)

**Output:** 7 -> 0 -> 8

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
  public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode f = new ListNode(0);
    ListNode p = f;

    int c = 0;

    while (l1 != null || l2 != null || c != 0) {
      int a = (l1 == null) ? 0 : l1.val;
      int b = (l2 == null) ? 0 : l2.val;
      int s = a + b + c;

      p.next = new ListNode(s % 10);
      p = p.next;

      if (l1 != null) l1 = l1.next;
      if (l2 != null) l2 = l2.next;

      c = s / 10;
    }

    return f.next;
  }
}
```