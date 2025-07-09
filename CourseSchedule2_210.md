- **Time Complexity:** O(V + E), where V is the number of courses and E is the number of prerequisite pairs.
- **Space Complexity:** O(V + E) for the graph and recursion stack.
- **Key Points:**
    - Topological Sort DFS algorithm
    - Build adjacency list to represent the grap and Load it for node (prerequisite course) as an index and index value as node (dependent courses) representing edges
    - Define an array to mark nodes (prerequisite course) visited
    - Visit each prerequisite node and perform DFS on adjacency list nodes
    - Check if cycle detected by check visited array value for given node

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();

        // Build adjacency list to represent the grap
        for (int i = 0; i < numCourses; i++) {
            graph.add(new ArrayList<>());
        }
        
        // Load adjacency list for node (prerequisite course) as an index and index value as node (dependent courses) representing edges
        // Why load dependent course as list values and not prerequisite node : Bcz need to push adj nodes by DFS into stack first and then prerequisite node so that it comes out first from stack and satisfy topological sort algorithm
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
        }

        // Define an array to mark nodes (prerequisite course) visited
        int[] visited = new int[numCourses];
        // stack to push nodes while DFS
        Stack<Integer> stack = new Stack<>();

        // Visit each prerequisite node and perform DFS on adjacency list nodes
        for (int i = 0; i < numCourses; i++) {
            if (dfs(i, graph, visited, stack)) {
                return new int[0]; // return if cycle detected
            }
        }
        
        int[] result = new int[numCourses];

        // Get nodes from stack which will give nodes in order as prerequisite requirement
        for (int i = 0; i < numCourses; i++) {
            result[i] = stack.pop();
        }

        return result;
    }

    private boolean dfs(int node, List<List<Integer>> graph, int[] visited, Stack<Integer> stack) {

        // cycle detected
        if (visited[node] == 1) return true;
        if (visited[node] == 2) return false;

        // Mark node as being visited for cycle detection check while adj list nodes being visited
        visited[node] = 1;

        for (int pre : graph.get(node)) {
            if (dfs(pre, graph, visited, stack)) return true; // cycle detected
        }

        visited[node] = 2; // node visited
        stack.push(node);
        return false;
    }
}
```