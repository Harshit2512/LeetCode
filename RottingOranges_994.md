- **Time Complexity:** O(m *n), where (m) is the number of rows and (n) is the number of columns. Each cell in the grid is processed at most once.
- **Space Complexity:** O(m * n) for the queue used in BFS.
- **Key Points:**
    - Load queue with initial all rotten oranges and find no of fresh oranges
    - Poll a queue for all rotten oranges loaded in a minute (till queue size) and get all adj rotten oranges and load then in queue
    - If at the end fresh oranges still left then return -1 (all oranges can't be rotten) or return total minutes (to rot all oranges)

```java
class Solution {
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        int freshOranges = 0;
        Queue<int[]> queue = new LinkedList<>();

        // adjecent dir coordinates
        int[] dx = {1, -1 , 0, 0};
        int[] dy = {0, 0, 1, -1};

        // Load all rotten oranges in the queue and count no of fresh oranges
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {    
                if (grid[r][c] == 2) queue.offer(new int[]{r, c});
                else if(grid[r][c] == 1) freshOranges++;  
            }
        }

        // initialize minute counter 
        int minutes = 0;

        // Apply BFS
        while (!queue.isEmpty() && freshOranges > 0) {
            minutes++;
            // total rotten oranges in a minute
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                int[] rotten = queue.poll();
                
                // for given rotten orange, iterate adj oranges and check if any fresh and load in a queue
                for (int d = 0; d < 4; d++) {
                    int newRow = rotten[0] + dx[d];
                    int newCol = rotten[1] + dy[d];

                    // rot fresh orange and put in a queue
                    if (newRow >= 0 && newCol >= 0 && newRow < rows && newCol < cols && grid[newRow][newCol] == 1) {
                        grid[newRow][newCol] = 2;
                        queue.offer(new int[]{newRow, newCol});
                        freshOranges--;
                    }
                }
            }
        }

        return freshOranges == 0 ? minutes : -1;
    }
}
```