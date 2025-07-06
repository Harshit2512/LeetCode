- **Time Complexity:** (O(m * n)), where m and n are the matrix dimensions. Each cell is processed at most once.
- **Space Complexity:** (O(m * n)), needed for the distance matrix and the BFS queue.
- **Key Points:**
    - Initialize result array with value as '0' for 0's and infinitive for 1's and put 1's cell in queue
    - Traverse in each dir from current cell and if new proposed value of cell is 1 greater then the current cell value then assign new proposed value (new distance) and put in queue for BFS

```java
class Solution {
    public int[][] updateMatrix(int[][] mat) {
        
        int rows = mat.length;
        int cols = mat[0].length;

        // Initialize new result array
        int[][] dist = new int[rows][cols];
        Queue<int[]> queue = new LinkedList<>();

        // Initialize result array with value as '0' for 0's and infinitive for 1's and put 1's in queue
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {    
                if (mat[r][c] == 0) {
                    dist[r][c] = 0;
                    queue.offer(new int[]{r, c});
                } else dist[r][c] = Integer.MAX_VALUE;
            }
        }

        int[][] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            int row = cell[0];
            int col = cell[1];

            for (int[] dir : dirs) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];

                if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols) {
                    // If new proposed value of cell is 1 greater then the current cell value then assign new proposed value (new distance) and put in queue for BFS
                    if (dist[newRow][newCol] > dist[row][col] + 1) {
                        dist[newRow][newCol] = dist[row][col] + 1;
                        queue.offer(new int[]{newRow, newCol});
                    }
                }
            }
        }
        return dist;
    }
}
```