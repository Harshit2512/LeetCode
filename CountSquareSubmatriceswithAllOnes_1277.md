- **Time Complexity:** (O(m * n)), where (m) and (n) are the dimensions of the matrix. Each cell is processed once.
- **Space Complexity:** (O(m * n)), additional space used for the DP matrix. 
- **Key Points:**
    - 2 D DP using top down approach
    - If first row or first col then use cell value as it is bcz prev left, top and digonal values are out of bound so only square of size 1 (cell itself) can be formed
    - If cell value is 1 then may be bigger square sub matrices be formed. Perform DP operation iteratively
    - After each iteration, add DP cell value to result var to get total count 

```java
class Solution {
    public int countSquares(int[][] matrix) {
        
        int m = matrix.length;
        int n = matrix[0].length;

        int[][] dp = new int[m][n];
        int count = 0;

        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                // If first row or first col then use cell value as it is bcz prev left, top and digonal values are out of bound so only square of size 1 (cell itself) can be formed
                if (r == 0 || c == 0) {
                    dp[r][c] = matrix[r][c];
                } else if (matrix[r][c] == 1) {
                    // If cell value is 1 then may be bigger square sub matrices be formed
                    // +1 is for cell formed itself added to count
                    dp[r][c] = 1 + Math.min(dp[r][c - 1], Math.min(dp[r - 1][c], dp[r - 1][c - 1]));
                }
                // Add to total count
                count += dp[r][c];
            }
        }

        return count;
    }
}
```