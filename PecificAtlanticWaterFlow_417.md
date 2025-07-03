- **Time Complexity:** (O(MN)), since each cell is processed twice (once for each ocean).
- **Space Complexity:** (O(MN)) for the space used by the two ocean-reachability matrices.
- **Key Points:**
    - Reverse thinking approach:
    - Maintain two boolean arrays to mark cells as reachable for both pecific and atlantic oceans 
    - Visit boundary cols and rows connected to pecific and atlantic oceans and run DFS
    - Mark cell as true for given (atlantic or pecific)
    - Iterate both boolean rachable arrays and for given row and col, if both are true then add in result list

```java
class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        
        int rows = heights.length;
        int cols = heights[0].length;

        boolean[][] pecReach = new boolean[rows][cols];
        boolean[][] atlReach = new boolean[rows][cols];

        // Visit boundary cols connected to pecific and atlantic oceans and run DFS
        for (int i = 0; i < rows; i++) {
            dfs(heights, pecReach, i , 0);
            dfs(heights, atlReach, i, cols - 1);
        }

        // Visit boundary rows connected to pecific and atlantic oceans and run DFS
        for (int j = 0; j < cols; j++) {
            dfs(heights, pecReach, 0 , j);
            dfs(heights, atlReach, rows - 1, j);
        }

        // Visit both reachable arrays and if for given cell, both are true then add in result list
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (pecReach[i][j] == true && atlReach[i][j] == true) {
                    result.add(Arrays.asList(i, j));
                }
            }
        }

        return result;
    }

    private void dfs(int[][] heights, boolean[][] reachable, int r, int c) {
        int rows = heights.length;
        int cols = heights[0].length;

        reachable[r][c] = true;

        int[][] dirs = {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};

        for (int[] dir : dirs) {
            int newRow = r + dir[0];
            int newCol = c + dir[1];

            if (newRow < 0 || newCol < 0 || newRow >= rows || newCol >= cols) continue; // out of bound
            if (reachable[newRow][newCol]) continue; // cell is already visited
            if (heights[r][c] > heights[newRow][newCol]) continue; // invalid height diff

            dfs(heights, reachable, newRow, newCol); 
        } 
    }
}
```