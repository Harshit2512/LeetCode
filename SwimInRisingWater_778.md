- **Time Complexity:** O(N^2 * log(N)), where N is the number of cells. The priority queue operations are logarithmic.
- **Space Complexity:** O(N^2) for visited structures and the priority queue storage. PQ could store duplicate value for same cell while iterating neighbors
- **Key Points:**
    - Djikstra algorithm to find shortest path (BFS)
    - Using MinHeap (water_level, x, y), traverse node and its neighbors while putting max of time came across so far
    - If bottom right corner cell is reached then return time else return default -1

```java
class Solution {
    public int swimInWater(int[][] grid) {
        int N  = grid.length;
        
        // Min heap -> (water_level, x, y)
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparing(a -> a[0]));
        boolean[][] visited = new boolean[N][N];
        int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

        pq.offer(new int[]{grid[0][0], 0, 0});

        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int time = curr[0];
            int x = curr[1];
            int y = curr[2];

            // if bottom right corner is reached then return time;
            if (x == N - 1 && y == N - 1) return time;
            if (visited[x][y]) continue;
            
            // Traverse all neighbors
            for (int[] dir : directions) {
                int dx = x + dir[0];
                int dy = y + dir[1];

                // Check boundry conditions
                if (dx >= 0 && dy >= 0 && dx < N && dy < N && !visited[dx][dy]) {
                    // Put max time took so far
                    pq.offer(new int[]{Math.max(time, grid[dx][dy]), dx, dy});
                    visited[x][y] = true;
                }
            } 
        }

        return -1;
    }
}
```