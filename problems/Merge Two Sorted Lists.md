# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

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
  public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode l = new ListNode(0);
    ListNode p = l;

    while (l1 != null || l2 != null) {
      if (l1 == null) {
        p.next = l2;
        break;
      }

      if (l2 == null) {
        p.next = l1;
        break;
      }

      if (l1.val < l2.val) {
        p.next = l1;
        l1 = l1.next;
      } else {
        p.next = l2;
        l2 = l2.next;
      }

      p = p.next;
    }

    return l.next;
  }
}
```