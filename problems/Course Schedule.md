# Course Schedule

There are a total of n courses you have to take, labeled from `0` to `n - 1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:
```
2, [[1,0]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.
```
2, [[1,0],[0,1]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Note:**

The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about how a graph is represented.

**Hints:**

1. This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2. Topological Sort via DFS - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.
3. Topological sort could also be done via BFS.

**Solution:**
```java
public class Solution {
  public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> adjList = new ArrayList<List<Integer>>(numCourses);

    for (int i = 0; i < numCourses; i++) 
      adjList.add(i, new ArrayList<Integer>());

    for (int i = 0; i < prerequisites.length; i++)
      adjList.get(prerequisites[i][0]).add(prerequisites[i][1]);

    boolean[] visited = new boolean[numCourses];

    for (int u = 0; u < numCourses; u++)
      if (hasCycle(adjList, u, visited, new boolean[numCourses]))
        return false;

    return true;
  }

  boolean hasCycle(List<List<Integer>> adjList, int u, boolean[] visited, boolean[] stack) {
    if (visited[u])
      return false;

    if (stack[u])
      return true;

    stack[u] = true;

    for (Integer v : adjList.get(u))
      if (hasCycle(adjList, v, visited, stack))
        return true;

    visited[u] = true;

    return false;
  }
}
```