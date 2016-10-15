# Remove Duplicates from Sorted List

Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,

Given `1->1->2`, return `1->2`.

Given `1->1->2->3->3`, return `1->2->3`.

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
  public ListNode deleteDuplicates(ListNode head) {
    ListNode p = head;

    while (p != null) {
      while (p.next != null && p.val == p.next.val) {
        p.next = p.next.next;
      }
      p = p.next;
    }

    return head;
  }
}
```