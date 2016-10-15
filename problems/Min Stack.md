# Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push(x) -- Push element x onto stack.
* pop() -- Removes the element on top of the stack.
* top() -- Get the top element.
* getMin() -- Retrieve the minimum element in the stack.

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

**Solution:**
```java
class MinStack {
  Stack<Integer> s1 = new Stack<>();
  Stack<Integer[]> s2 = new Stack<>();

  public void push(int x) {
    s1.push(x);
    if (s2.isEmpty() || x < s2.peek()[0]) {
      s2.push(new Integer[]{x, 1});
    } else if (x == s2.peek()[0]) {
      s2.peek()[1]++;
    }
  }

  public void pop() {
    if (s1.peek().intValue() == s2.peek()[0]) {
      s2.peek()[1]--;
      if (s2.peek()[1] == 0)
        s2.pop();
    }
    s1.pop();
  }

  public int top() {
    return s1.peek();
  }

  public int getMin() {
    return s2.peek()[0];
  }
}
```