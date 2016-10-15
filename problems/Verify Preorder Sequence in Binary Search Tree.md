# Verify Preorder Sequence in Binary Search Tree

Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

You may assume each number in the sequence is unique.

**Follow up:**

Could you do it using only constant space complexity?

**Solution:**
```java
public class Solution {
  public boolean verifyPreorder(int[] preorder) {
    int low = Integer.MIN_VALUE;
    Stack<Integer> path = new Stack();

    for (int p : preorder) {
      if (p < low)
        return false;

      // If the current value is larger, we are going to the right
      // because of preorder, the numbers afterwards cannot be less
      // than the ones in the stack
      while (!path.empty() && p > path.peek())
        low = path.pop();

      path.push(p);
    }

    return true;
  }
}
```
