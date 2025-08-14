- **Time Complexity:** O(m * n): We explore each cell once, memoizing the results, thus preventing redundant computations.
- **Space Complexity:** O(m * n): The space due to recursive stack and memoization table.
- **Key Points:**
    - DP - Memoization approach, define memo 2D array as same length of input matrix
    - For each cell, perform DFS. Move to all 4 dirs ad if next cell value is in increasing order then perform DFS.
    - Calculate max length (LIP) for each cell once all 4 directional recursive call completes
    - Keep updating result s max LIP for each matrix cell

```java
class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        int[][] dp = new int[m][n];

        int[][] dirs = new int[][]{{1, 0}, {0, 1}, {-1, 0}, {0, -1}};

        int result = 0;

        // Iterate each cell to run DFS on
        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {    
                result = Math.max(result, 1 + dfs(r, c, matrix, dp, dirs));
            }
        }

        // Return max length calculated
        return result;
    }

    private int dfs(int r, int c, int [][] matrix, int[][] dp, int[][] dirs) {
        // If cell in Dp array is not 0, then we have already visited cell and can reuse prev computed max LIP from that cell
        if (dp[r][c] != 0) {
            return dp[r][c];
        }

        int maxLength = 0;

        // DFS in all four dirs from cell
        for (int[] dir : dirs) {
            int x = r + dir[0];
            int y = c + dir[1];
   
            if (x >= 0 && y >= 0 && x < matrix.length && y < matrix[0].length && matrix[x][y] > matrix[r][c]) {
                // Perform DFS on each directional cell
                // +1 : increase path length created by current cell to prev created path length if next cell cell is increasing order
                maxLength = Math.max(maxLength, 1 + dfs(x, y, matrix, dp, dirs));
            }
        }

        // once recusrsively travelled in all 4 dirs and got possible LIP, assign it to DP array
        // It says that at this cell tehre are x path length
        dp[r][c] = maxLength;

        return maxLength;       
    }
}
```