# LRU Cache

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

* `get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.

* `set(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Solution:**
```java
public class LRUCache {
    
  int capacity;
  Map<Integer, ListNode> map;
  ListNode head;
  ListNode tail;

  public LRUCache(int cap) {
    capacity = cap;
    map = new HashMap<>();
    head = new ListNode(0, 0);
    tail = new ListNode(0, 0);
    head.next = tail;
    tail.prev = head;
  }

  public int get(int key) {
    if (!map.containsKey(key)) {
      return -1;
    }

    ListNode node = map.get(key);
    promote(node);
    return node.val;
  }

  public void set(int key, int val) {
    ListNode node;

    if (map.containsKey(key)) {
      node = map.get(key);
      promote(node);
      node.val = val;
      return;
    }

    if (map.size() == capacity) {
      ListNode last = tail.prev;
      map.remove(last.key);
      remove(last);
    }

    node = new ListNode(key, val);
    map.put(key, node);
    insert(node);
  }

  void remove(ListNode node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
  }

  void insert(ListNode node) {
    node.prev = head;
    node.next = head.next;
    head.next.prev = node;
    head.next = node;
  }

  void promote(ListNode node) {
    remove(node);
    insert(node);
  }

  class ListNode {
    int key;
    int val;
    ListNode prev = null;
    ListNode next = null;

    public ListNode(int k, int v) {
      key = k;
      val = v;
    }
  }
    
}
```