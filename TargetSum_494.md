```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        
        // The transformed problem only makes sense if the sum can accommodate the target
        if (sum < target || (target + sum) % 2 != 0) {
            return 0;
        }
        
        int targetSum = (target + sum) / 2;
        if (targetSum < 0) {
            return 0;
        }
        return subsetSum(nums, targetSum);
    }
    
    private int subsetSum(int[] nums, int targetSum) {
        int[] dp = new int[targetSum + 1];
        dp[0] = 1; // There's one way to have a sum of 0, which is picking nothing
        
        for (int num : nums) {
            for (int j = targetSum; j >= num; j--) {
                dp[j] += dp[j - num];
            }
        }
        
        return dp[targetSum];
    }
}
```