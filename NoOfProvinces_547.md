- **Time Complexity:** O(n^2): We visit each cell in the matrix isConnected exactly once.
- **Space Complexity:** O(n): The space for the visited array and the call stack in the worst case (when the graph is a single connected component).
- **Key Points:**
    - The problem can be conceptualized as finding connected components in an undirected graph. Each city is a node, and a direct road between two cities is an edge. Each new unvisited node indicates the start of a new province.
    - Visit each city if not visited and visit all connected cities by performing DFS
    - Visit city's connected cities if not already visited

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int provinces = 0;

        for (int i = 0; i < n; i++) {
            // Visit each city if not visited and visit all connected cities by performing DFS
            if (!visited[i]) {
                dfs(isConnected, visited, i);
                provinces++;
            }
        }

        return provinces;
    }

    private void dfs(int[][] isConnected, boolean[] visited, int city) {
        visited[city] = true;

        // Visit city's connected cities if not already visited
        for (int i = 0; i < isConnected.length; i++) {
            if (isConnected[city][i] == 1 && !visited[i]) {
                dfs(isConnected, visited, i);
            }
        }
    }
}
```