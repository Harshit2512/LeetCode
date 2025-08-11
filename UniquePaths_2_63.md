- **Time Complexity:** O(m*n) — We iterate through each cell once.
- **Space Complexity:** O(n) — Space for the 1-D dp array.
- **Key Points:**
    - Space optimization approach using 1 D DP array
    - Since we only need to look for row below, we don't need to preserve all rows. Prev row will keep getting updated from it's row above
    - If we hit obstacle then update DP element at that COL (same col from row above - one layer up row)
    - If no obstacle then update DP element using DP logic and return last element of the DP as result

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;

        // Define DP array of row size of input
        int[] dp = new int[n];

        // Fill first cell with value
        dp[0] = obstacleGrid[0][0] == 0 ? 1 : 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // if given cell has obstacle then assign dp value as 0 mean no path avaiable
                if (obstacleGrid[i][j] == 1) {
                    dp[j] = 0;
                } else if (j > 0) {
                    // dp[j] = bottom value: value of same col from row below
                    // dp[j - 1] = left col value from same row
                    dp[j] = dp[j] + dp[j-1];
                }
            }
        }

        return dp[n - 1];
    }
}
```