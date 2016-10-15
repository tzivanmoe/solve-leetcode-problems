# Remove Linked List Elements

Remove all elements from a linked list of integers that have value val.

Example

Given: `1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6`, val = `6`

Return: `1 --> 2 --> 3 --> 4 --> 5`

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
  public ListNode removeElements(ListNode head, int val) {
    if (head == null)
      return null;

    ListNode f = new ListNode(0);
    ListNode p = f;

    while (head != null) {
      if (head.val != val) {
        p.next = head;
        p = p.next;
      }
      head = head.next;
    }

    p.next = null;

    return f.next;
  }
}
```