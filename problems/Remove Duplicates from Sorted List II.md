# Remove Duplicates from Sorted List II

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,

Given `1->2->3->3->4->4->5`, return `1->2->5`.

Given `1->1->1->2->3`, return `2->3`.

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
    if (head == null) {
      return null;
    }

    ListNode fake = new ListNode(0);
    ListNode p = fake;
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null) {
      int count = 0;

      while (fast != null && fast.val == slow.val) {
        count++;
        fast = fast.next;
      }

      if (count == 1) {
        p.next = slow;
        p = p.next;
      }

      slow = fast;
    }

    p.next = null;

    return fake.next;
  }
}
```