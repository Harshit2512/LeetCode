- **Time Complexity:** O(n^3) because of the two nested loops and substring check. O(n^2) for nested for loop and O(n) for substring creation in java considering SS could be full string in worst case
- **Space Complexity:** O(n) for the dp array.
- **Key Points:**
    - Convert list to set for O(1) look-up times
    - Check each possible end-point for substrings. end is for outer boundary and start is for SS start index
    - If the start point is breakable (prev SS can be segmented) and the substring s[start:end] is in the dictionary. If SS is found then update DP[end] to true meaning word could be segmented
    - The result for the whole string is in dp[n]

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<>(wordDict); // Convert list to set for O(1) look-up times
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true; // Base case: an empty string is "breakable"
        
        // Check each possible end-point for substrings
        // end = outer boundary of substring
        for (int end = 1; end <= s.length(); end++) {
            // start = start position of substring
            for (int start = 0; start < end; start++) {
                // If the start point is breakable and the substring s[start:end] is in the dictionary
                // dp[start] == true → means prefix s[0..start-1] can be segmented.
                // s[start:end] is in dictionary → the current substring is a valid word.
                // If both hold, then s[0..end-1] can be segmented → set dp[end] = true.
                if (dp[start] && wordSet.contains(s.substring(start, end))) {
                    dp[end] = true;
                    break; // No need to check further substrings if we found one that works
                }
            }
        }
        
        return dp[s.length()]; // The result for the whole string is in dp[n]
    }
}
```