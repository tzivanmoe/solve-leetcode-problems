# Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

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
  public ListNode mergeKLists(ListNode[] lists) {
    ListNode f = new ListNode(0);
    ListNode p = f;

    int k = lists.length;

    PriorityQueue<ListNode> heap = new PriorityQueue<>(k + 1, new Comparator<ListNode>() {
      public int compare(ListNode a, ListNode b) {
        return a.val - b.val;
      }
    });

    // step 1. put the first node of every list to the min heap
    for (int i = 0; i < k; i++) {
      if (lists[i] != null) {
        heap.offer(lists[i]);
      }
    }

    while (!heap.isEmpty()) {
      ListNode node = heap.poll();

      p.next = node;
      p = p.next;

      if (node.next != null) {
        heap.offer(node.next);
      }
    }

    p.next = null;
    return f.next;
  }
}
```