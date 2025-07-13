- **Time Complexity:** O(V^2 log V), where V is the number of vertices. Each vertex can potentially have an edge to all other vertices so there can be duplicate edge to that vertex and each operation in priority queue is log V.
- **Space Complexity:** O(V), storing minimum distances and mark arrays.
- **Key Points:**
    - problem can be translated into finding a Minimum Spanning Tree (MST) of a graph
    - Initialize all variables for Prim's algorithm to track visited nodes, PQ and array to track min distance edge for node
    - Start from (0,0) and consider all edges from point and iterate (BFS) to find edge with min dist to target point
    - Find distance to traget point and if dist to this point is minimum then update distance and add pair {point, dist} in the heap

```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        boolean[] visited = new boolean[n]; // array to track the points already visited
        PriorityQueue<int[]> minHeap = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        int minCost = 0;
        int[] minDistToPoint = new int[n];
        Arrays.fill(minDistToPoint, Integer.MAX_VALUE);
        minDistToPoint[0] = 0;

        // Initial point to begin with {0,0}
        minHeap.offer(new int[]{0, 0});

        while (!minHeap.isEmpty()) {
            // take distance edge from heap
            int[] minEdge = minHeap.poll();
            int point = minEdge[0];

            // if point is already visited then skip this edge
            if (visited[point]) continue;

            minCost += minEdge[1];
            visited[point] = true;

            // iterate all edges from this current point (BFS) and find distance, push edge with min distance (cost) to heap
            for (int v = 0; v < n; v++) {
                if (!visited[v]) {
                    // If min dist to this point is minimum then update distance and add pair {point, dist} in the heap
                    int dist = Math.abs(points[point][0] - points[v][0]) + Math.abs(points[point][1] - points[v][1]);
                    if (dist < minDistToPoint[v]) {
                        minDistToPoint[v] = dist;
                        minHeap.offer(new int[]{v, dist});
                    }
                }
                
            }

        } 

        return minCost;
    }
}
```