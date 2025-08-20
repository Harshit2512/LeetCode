- **Time Complexity:** O(n^2) for filling the entire dp table.
- **Space Complexity:** O(n^2) for the dp table storage.
- **Key Points:**
    - Bottom-up dynamic programming approach - can also be solved as extention of longest common subsequence problem with two strings
    - Subsequence(can drop any char but order remains same) vs substring(can't drop any char):
    - All chars alone make a palindrom subsequence of 1. So fill matrix diagonal with 1
    - len is the length of substring we take to find palindrom SS. start with 2 (min 2 char unto full string length)
    - For each length of len, iterate all combination of substring of 2 chars
    - If first (i) and end (j) char of window match then they both can create subsequence of atleast 2 so add 2 and move inwards for all possible SS with window
    - Choose the longer subsequence after excluding each character (one from start keeping end and then one from end keeping start)
    - last cell in first row will give longest palindromic ss calculated

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        // s = bbbab
        int n = s.length();
        int[][] dp = new int[n][n];

        // all chars alone make a palindrom subsequence of 1. So fill matrix diagonal with 1
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

        // len is the length of substring we take to find palindrom SS. start with 2 (min 2 char unto full string length)
        for (int len = 2; len <= n; len++) {
            // for each length of len, iterate all combination of substring of 2 chars
            // len = 2 -> bb, bb, ba, ab
            // len = 3 -> bbb, bba, bab
            for (int i = 0; i <= n - len; i++) {
                int j = i + len - 1;

                // If first (i) and end (j) char of window match then they both can create subsequence of atleast 2 so add 2
                // add SS made by diogonal cell (each individual char) into 2 and move inwards for all possible SS with window
                // 
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = 2 + dp[i + 1][j - 1];
                } else {
                    // Choose the longer subsequence after excluding each character (one from start keeping end and then one from end keeping start)
                    // ex: bba -> drop first char b and take ba to find ss, and drop last char a and take bb to find ss
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }

        // last cell in first row will give longest palindromic ss calculated 
        return dp[0][n - 1];
    }
}
```