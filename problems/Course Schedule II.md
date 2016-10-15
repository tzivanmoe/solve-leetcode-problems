# Course Schedule II

There are a total of n courses you have to take, labeled from `0` to `n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:
```
2, [[1,0]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is `[0,1]`
```
4, [[1,0],[2,0],[3,1],[3,2]]
```
There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is `[0,1,2,3]`. Another correct ordering is `[0,2,1,3]`.

**Note:**

The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about how a graph is represented.

**Hints:**

1. This problem is equivalent to finding the topological order in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2. Topological Sort via DFS - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
3. Topological sort could also be done via BFS.

**Solution:**
```java
public class Solution {
  public int[] findOrder(int numCourses, int[][] prerequisites) {
    // Use adjacency list
    List<List<Integer>> adj = new ArrayList<List<Integer>>(numCourses);

    for (int i = 0; i < numCourses; i++)
      adj.add(i, new ArrayList<>());

    for (int i = 0; i < prerequisites.length; i++) 
      adj.get(prerequisites[i][1]).add(prerequisites[i][0]);

    boolean[] visited = new boolean[numCourses];

    // reverse result of dfs is the answer
    Stack<Integer> stack = new Stack<>();

    for (int u = 0; u < numCourses; u++) {
      if (!topologicalSort(adj, u, stack, visited, new boolean[numCourses])) 
        return new int[0];
    }

    int i = 0;
    int[] result = new int[numCourses];
    while (!stack.isEmpty()) {
      result[i++] = stack.pop();
    }
    return result;
  }

  private boolean topologicalSort(List<List<Integer>> adj, int u, Stack<Integer> stack, boolean[] visited, boolean[] isLoop) {
    if (visited[u]) 
      return true;

    if (isLoop[u]) 
      return false;

    isLoop[u] = true;

    for (Integer v : adj.get(u)) {
      if (!topologicalSort(adj, v, stack, visited, isLoop)) 
        return false;
    }

    visited[u] = true;

    stack.push(u);
    return true;
  }
}
```