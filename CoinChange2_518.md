- **Time Complexity:** O(n * amount), where n is the number of coins.
- **Space Complexity:** O(amount), optimal space usage with a 1D array.
- **Key Points:**
    - Approach: Dynamic programing using 1 D array, Define DP array with size amount + 1. +1 comes from accomodating size of array
    - Take each coin, for each coin update no of ways to make j amount
    - dp[j] += dp[j - coin] dynamically accumulates the number of ways to build amount j using the current coin.
    - Each update reflects: “If I can make amount j - coin, then I can also make j by adding this coin.”

```java
class Solution {
    public int change(int amount, int[] coins) {
        // DP array says how many diff ways amount can be achieved
        int[] dp = new int[amount + 1];
        // Amount 0 can be chossen in 1 way, by not choosing any coin
        dp[0] = 1;

        for (int coin : coins) {
            for (int j = coin; j <= amount; j++) {
                // by choosing coin and subtracting it's value from j, add j - coin ways to dp[j] to get total no of ways to reach to j amount
                // The number of ways to make amount j is increased by the number of ways to make amount j - coin.
                // dp[j] += dp[j - coin] dynamically accumulates the number of ways to build amount j using the current coin.
                // Each update reflects: “If I can make amount j - coin, then I can also make j by adding this coin.”
                dp[j] += dp[j - coin];
            }
        }

        return dp[amount];
    }
}
```