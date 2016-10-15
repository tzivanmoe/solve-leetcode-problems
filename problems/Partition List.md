# Partition List

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,

Given `1->4->3->2->5->2` and x = 3,

return `1->2->2->4->3->5`.

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
  public ListNode partition(ListNode head, int x) {
    if (head == null) {
      return null;
    }

    // create fake heads
    ListNode f1 = new ListNode(0);
    ListNode f2 = new ListNode(0);

    ListNode p1 = f1;
    ListNode p2 = f2;

    ListNode node = head;
    while (node != null) {
      if (node.val < x) {
        p1.next = node;
        p1 = p1.next;
      } else {
        p2.next = node;
        p2 = p2.next;
      }
      node = node.next;
    }

    p1.next = f2.next;
    p2.next = null;

    return f1.next;
  }
}
```