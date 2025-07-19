- **Time Complexity:** O(n), each step is calculated once in a loop.
- **Space Complexity:** O(1), using constant space for last two computed states.
- **Key Points:**
    - Use dynamic programing optimization approach which uses two pointers to optimize space
    - This problem is presentation of fibonacci sequence
    - We use space memoization which uses the already solved sub problem result
    - This uses bottom up approach

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) return 1;
        int oneStep = 1;
        int twoStep = 1;
        
        for (int i = 2; i <= n; i++) {
            int allWays = oneStep + twoStep;
            twoStep = oneStep;
            oneStep = allWays;
        }

        return oneStep; 
    }
}
```