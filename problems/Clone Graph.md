# Clone Graph

Clone an undirected graph. Each node in the graph contains a **label** and a list of its **neighbors**.

**OJ's undirected graph serialization:**
Nodes are labeled uniquely.

We use **#** as a separator for each node, and **,** as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph **{0,1,2#1,2#2,2}**.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

1. First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
2. Second node is labeled as 1. Connect node 1 to node 2.
3. Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.


Visually, the graph looks like the following:
```
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```

**Solution:**
```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
  public UndirectedGraphNode cloneGraph(UndirectedGraphNode root) {
    if (root == null) return null;

    // use a map to save cloned nodes
    Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();

    // clone the root
    map.put(root, new UndirectedGraphNode(root.label));

    helper(root, map);

    return map.get(root);
  }

  void helper(UndirectedGraphNode root, Map<UndirectedGraphNode, UndirectedGraphNode> map) {
    for (UndirectedGraphNode neighbor : root.neighbors) {
      if (!map.containsKey(neighbor)) {
        map.put(neighbor, new UndirectedGraphNode(neighbor.label));
        helper(neighbor, map);
      }

      map.get(root).neighbors.add(map.get(neighbor));
    }
  }
}
```