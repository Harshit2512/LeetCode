- **Time Complexity:** O(n * s) - where n is number of elements in the array and s is half the total sum of all elements.
- **Space Complexity:** O(s) - this is space used by the dp array.
- **Key Points:**
    - Optimal solution using DP approach
    - If total sum is divisible by 2 then there are two subset from array which sum up to target value
    - Maintain dp array to decide if two subsets can be made
    - dp[s] = dp[s] || dp[s - num] -> dp[s - num] == true means: there is a subset (from previously considered numbers) that adds up to s - num

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }

        // If total sum is divisible by 2 then there are two subset from array which sum up to target value
        if (totalSum % 2 != 0) return false;
        int target = totalSum / 2;

        // Maintain dp array to decide if two subsets can be made
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;

        for (int num : nums) {
            for (int s = target; s >= num; s--) {
                // assign dp[s] to true/false based on dp[s] or dp[s - num]
                // If we can form a subset with sum s - num, then we can also form a subset with sum s by including num.
                // dp[s - num] == true means: there is a subset (from previously considered numbers) that adds up to s - num
                dp[s] = dp[s] || dp[s - num];
            }
        }
        return dp[target];
    }
}
```