- **Time Complexity:** O(N), visit all graph nodes exactly once
- **Space Complexity:** O(N), use array to maintain if node is visited(colored) before
- **Key Points:**
    - Bipartite graph: if its nodes can be divided into two independent sets such that no two graph nodes within the same set are adjacent.
    - Use two color technique to color node and it's neighbours using DFS
    - Use array to keep track of node visit. If node/neighbour is not visited before then visit(color) it and run DFS on neighbours
    - If node is visited(colored) before then check it's any of it's neighbour doesn't have same color. If has has color the non-bipartite

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] colors = new int[n];
        Arrays.fill(colors, -1);

        // Iterate each node and color it if not colored (visited)
        for (int i = 0; i < n; i++) {
            // If node is not visited (colored) then visit node
            if (colors[i] == -1) {
                if (!dfs(graph, colors, i, 1)) {
                    return false;
                }
            }
        }
        return true;
    }

    private boolean dfs(int[][] graph, int[] colors, int node, int color) {

        // Color the node
        colors[node] = color;

        // Visit all neighbours of node and run DFS to visit(color) them
        for (int nei : graph[node]) {
            // If neighbour is not visited before then visit it and run DFS on neighbour
            if (colors[nei] == -1) {
                if (!dfs(graph, colors, nei, 1 - color)) {
                    return false;
                }
            }

            // If neiggbour is already visited then check if it has same color, if same color then graph is not bipartite
            else if (colors[nei] == color) {
                return false;
            }
        }

        return true;
    }
}
```