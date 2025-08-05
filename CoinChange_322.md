- **Time Complexity:** O(S * n) where S is the amount and n is the number of coins.
- **Space Complexity:** O(S) for the DP table.
- **Key Points:**
    - Optimized approach using dynamic programming - Pattern - Target is given and asked to find optimum selection  which sum up to target
    - Define DP array of size amount
    - Iterate all coins one by one and if coin amount is less than current amount, add coin count by 1
    - Return DP array element at index amount(target)

```java
class Solution {
    public int coinChange(int[] coins, int amount) {

        // amount + 1 is for setting dp array size
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0; // Base case: zero coins needed for zero amount

        for (int i = 1; i <= amount; i++) {
            for (int coin: coins) {
                if (coin <= i) { // If coin value is less than amount then only we can substract from amount
                // +1 is for increase coin count by +1 when added
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }            
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```