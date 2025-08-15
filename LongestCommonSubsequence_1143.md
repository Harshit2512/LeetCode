- **Time Complexity:** O(m * n)
- **Space Complexity:** O(m * n)
- **Key points:**
    - (word doc) Perform DP (bottom-up) on string using 2D array with +1 sizes of both strings
    - Iterate each chars using nested for loops to read all chars
    - If char at index from both strings are same read diagonal value from DP table and add 1 for current match
    - If chars at index don't match then take max of one row up an one col left value from DP table
    - Return value at DP[text1 length][text2 length]

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();

        // Why +1 : To accomodate the leth of empty string. Also while ready first row or col, we need to have something (dummy row or col with value) up or left or diagonally to read 
        // Define DP array initially all filled with 0
        int[][] dp = new int[m+1][n+1];

        // why start from 1 : we have row 0 and col 0 assigned for dummy values to read prev dp value left, up and diagonaly
        // Start reading from starting of both strings
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                // If char at index from both strings are same read diagonal value from DP table and add 1 for current match
                // Why diagonal? : If characters match, we extend the LCS from the previous subproblem (both strings one character shorter)
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    // Take diagonal value from DP table
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    // If chars at index don't match then take max of one row up an one col left value from DP table 
                    // Removing the current character from text1 → dp[i-1][j] and Removing the current character from text2 → dp[i][j-1]

                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }
}
```