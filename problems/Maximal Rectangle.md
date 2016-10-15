# Maximal Rectangle

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing all ones and return its area.

**Solution:**
```java
public class Solution {
  public int maximalRectangle(char[][] M) {
    if (M == null || M.length == 0 || M[0].length == 0) {
	  return 0;
    }
		
    int max = 0;
	int m = M.length;
	int n = M[0].length;
		
	int[][] H = new int[m][n];
		
	for (int i = 0; i < m; i++) {
	  for (int j = 0; j < n; j++) {
	    int v = getInt(M[i][j]);
				
		if (i == 0 || v == 0) {
		  H[i][j] = v;
		} else {
		  H[i][j] = v + H[i - 1][j];
		}
	  }
			
	  int res = largestRectangleArea(H[i]);
			
	  max = Math.max(max, res);
	}
		
	return max;
  }
    
  public int largestRectangleArea(int[] A) {
    if (A == null) {
	  return 0;
	}
		
	Stack<Integer> stack = new Stack<Integer>();
		
	int n = A.length, max = 0;
		
	for (int i = 0; i < n; i++) {
	  while (!stack.isEmpty() && A[i] <= A[stack.peek()]) {
	    int index = stack.pop();
		int left = stack.isEmpty() ? 0 : stack.peek() + 1;
				
		max = Math.max(max, A[index] * (i - left));
	  }
			
	  stack.push(i);
    }
		
	while (!stack.isEmpty()) {
	  int index = stack.pop();
	  int left = stack.isEmpty() ? 0 : stack.peek() + 1;
			
	  max = Math.max(max, A[index] * (n - left));
    }
		
	return max;
  }
    
  private int getInt(char ch) {
    return (int)(ch - '0');
  }
}
```