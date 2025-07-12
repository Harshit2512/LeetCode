- **Time Complexity:** O(N), where N is the number of edges. Each find and union operation runs in near constant time thanks to the path compression and union by rank heuristics.
- **Space Complexity:** O(N), for storing parent and rank arrays in the DSU structure.
- **Key Points:**
    - Initialize a Union-Find structure for n elements. Iterate through each edge.
    - For each edge, check if the two endpoints are in the same component (parent of itself) using find with path compression along the way
    - Perform union by rank to check if edge can't be union and creates a cycle

```java
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        
        int n = edges.length;
        DSU dsu = new DSU(n);

        // iterate all edges and check for cycle by disjoint union find
        for (int[] edge : edges) {
            if (!dsu.union(edge[0] - 1, edge[1] - 1)) {
                // if return true, mean edge u and v is creating cycle
                return edge;
            }
        }
        // if cycle  not found, return default edge with size 2
        return new int[2];
    }

    class DSU {
        int[] parent;
        int[] rank;

        public DSU(int size) {
            parent = new int[size];
            rank = new int[size];

            for (int i = 0; i < size; i++) {
                parent[i] = i;
                rank[i] = 1;
            }
        }

        public int find(int u) {
            // if node is not parent of itself
            if (parent[u] != u) {
                // path compression along the way finding the parent
                parent[u] = find(parent[u]);
            }
            return parent[u];
        }

        public boolean union(int u, int v) {
            int rootU = find(u);
            int rootV = find(v);

            // if u and v has same root, then already part of same component and form a cycle
            if (rootU == rootV) {
                return false;
            }

            // Union find by rank
            if (rank[rootU] > rank[rootV]) {
                parent[rootV] = rootU; 
            } else if (rank[rootU] < rank[rootV]) {
                parent[rootU] = rootV;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++; 
            }

            return true;
        }
    }
}
```