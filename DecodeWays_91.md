- **Time Complexity:** (O(N)), iterating through the string once.
- **Space Complexity:** (O(N)), for the dp array.
- **Key Points: word doc**
    - Define DP with size n+1 : dp[0] = 1 refers for no of ways to decode empty string
    - dp[i] represents no of ways to decode for upto i prefix string
    - s.charAt(0) : If string has leading zero then it can't be decoded
    - For prefix length 1, check i-1 for i
    - For prefix length 2, check [i-2, i-1] creates no less than 26 (max Z = 26)
    - dp[n] represents summed up no of ways to decode
    - https://chatgpt.com/share/68a7991c-a82c-8002-a0aa-e4fffd0e8c8e

```java
class Solution {
    public int numDecodings(String s) {
        int n = s.length();
        // DP: size n + 1 -> dp[0] is for for decoding the empty string
        // dp[i] -> no of way to decode string upto i (prefix string)

        int[] dp = new int[n+1];
        dp[0] = 1; //empty string is decoded in exact one way

        // s.charAt(0) : If string has leading zero then it can't be decoded
        if (s == null || s.length() == 0 || s.charAt(0) == '0') return 0;

        // start from i = 1 bcz i = 0 is for empty prefix
        for (int i = 1; i <= n; i++) {
            if (s.charAt(i - 1) != '0' ) {
                // add prev ways to no of ways for upto i 
                dp[i] = dp[i] + dp[i - 1];
            }

            // check for two chars string which can be decoded from '10' to '26'
            if (i > 1 && (s.charAt(i - 2) == '1' || (s.charAt(i - 2) == '2' && s.charAt(i - 1) <= '6'))) {
                dp[i] = dp[i] + dp[i - 2];
            }
        } 

        // dp value at string length returns summed up no of ways to decode
        return dp[n];  
    }
}
```