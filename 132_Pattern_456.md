- **Time Complexity:** O(n), since each element is pushed and popped from the stack at most once.
- **Space Complexity:** O(n), for the stack used to store potential nums[j] candidates.
- **Key Points:**
    - Monotonic stack condition : (nums[i] > stack.peek()) --> checks whether for given j < k, can nums[k] < nums[j] ?

``` java
class Solution {
    public boolean find132pattern(int[] nums) {
        
        // thirdK is to track the index k's value which could be less that nums[j] and greater that nums[i]
        int thirdK = Integer.MIN_VALUE;
        Stack<Integer> stack = new Stack<>();

        for (int i = nums.length -1; i >= 0; i--) {
            
            // If any value found which is less than k, that means 132 pattern exist
            if (nums[i] < thirdK) {
                return true;
            }

            // nums[i] > stack.peek() --> checks whether for given j < k, can nums[k] < nums[j] ?
            while(!stack.isEmpty() && nums[i] > stack.peek()) {
                thirdK = stack.pop();
            }

            stack.push(nums[i]);
        }

        return false;
    }
}
```