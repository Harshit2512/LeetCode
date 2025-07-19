- **Time Complexity:** O(n), linear traversal of array.
- **Space Complexity:** O(1), space usage is constant due to only using fixed variables for calculations.
- **Key Points:**
    - Rob houses from index 0 to n-2 (excluding the last house). Rob houses from index 1 to n-1 (excluding the first house).

```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 1) return nums[0];
        return Math.max(robRange(nums, 0, nums.length - 2), robRange(nums, 1, nums.length - 1));
    }

    private int robRange(int[] nums, int start, int end) {
        int prev1 = 0; // Store the result of i-1
        int prev2 = 0; // Store the result of i-2
        for (int i = start; i <= end; i++) {
            int temp = Math.max(prev1, prev2 + nums[i]);
            // Move previous results one step forward
            prev2 = prev1;
            prev1 = temp;
        }
        return prev1;
    }
}
```