- **Time Complexity:** (O(M * N)) where M is the number of rows and N is the number of columns.
- **Space Complexity:** (O(M * N)) in worst case for the recursion stack.
- **Key Points:**
    - For each cell in grid, if gound '1', use DFS to traverse all cells in four directions
    - Mark visited cell as 0 to not visit them again

```java
class Solution {
    public int numIslands(char[][] grid) {

        if (grid == null || grid.length == 0) {
            return 0;
        }

        int rows = grid.length;
        int cols = grid[0].length;
        int numIslands = 0;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == '1') {
                    numIslands++;
                    dfs(grid, i, j);
                }
            }
        }
        return numIslands;
    }

    private void dfs(char[][] grid, int r, int c) {
        int rows = grid.length;
        int cols = grid[0].length;

        if (r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] == '0') {
            return;
        }

        // Mark cell as visited
        grid[r][c] = '0';

        // visit neighbouring cells in four directions
        dfs(grid, r + 1, c);
        dfs(grid, r - 1, c);
        dfs(grid, r, c + 1);
        dfs(grid, r, c - 1);
    }
}
```