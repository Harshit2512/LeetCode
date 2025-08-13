- **Time Complexity:** O(m*n) as we iterate over each cell exactly once.
- **Space Complexity:** O(1) since we use the input grid itself to store minimum path sums.
- **Key Points:**
    - Inplace DP using space optimization approach - bottom up
    - Instead of defining separate DP array, replace value in place in input array
    - Start from last cell (bootom-right) and move to first cell
    - If at last row then we can only read from right col (column shift), if at last col then we can only read from below row (row shift)
    - Read min value from either right or below from current cell and finally return grid[0][0] as answer that has minimum path sum

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        for (int r = m - 1; r >= 0; r--) {
            for (int c = n - 1; c >= 0; c--) {

                // if at the bottom right last cell then continue
                if (r == m - 1 && c == n - 1) continue;

                // if at last row then we can only read from right col (column shift)
                if (r == m - 1) {
                    grid[r][c] = grid[r][c] + grid[r][c + 1];
                }

                // if at last col then we can only read from below row (row shift)
                else if (c == n - 1) {
                    grid[r][c] = grid[r][c] + grid[r + 1][c];
                }

                // read min value from either right or below from current cell
                else {
                    grid[r][c] = grid[r][c] + Math.min(grid[r + 1][c], grid[r][c + 1]);
                }
            }
        }

        // return first cell (bottom-up approach)
        return grid[0][0];
    }
}
```