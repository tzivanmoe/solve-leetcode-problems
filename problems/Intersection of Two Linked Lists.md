# Intersection of Two Linked Lists

Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.


**Notes:**

* If the two linked lists have no intersection at all, return null.
* The linked lists must retain their original structure after the function returns.
* You may assume there are no cycles anywhere in the entire linked structure.
* Your code should preferably run in O(n) time and use only O(1) memory.

**Solution:**
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
  public ListNode getIntersectionNode(ListNode l1, ListNode l2) {
    if (l1 == null || l2 == null) return null;

    // step 1. count the two lists
    int n1 = count(l1), n2 = count(l2);

    // step 2. move the longer one |n2 - n1| steps
    int n = Math.abs(n1 - n2);

    while (n-- > 0) {
      if (n1 > n2) 
        l1 = l1.next;
      else
        l2 = l2.next;
    }

    // step 3. move together and find the meeting point
    while (l1 != l2) {
      l1 = l1.next;
      l2 = l2.next;
    }

    return l1;
  }

  int count(ListNode l) {
    if (l == null) return 0;
    return 1 + count(l.next);
  }
}
```