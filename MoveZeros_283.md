- **Time Complexity:** O(N), N is length of the array
- **Space Complexity:** O(1)
- **Approach:** using two pointers - Fixed window
    - Two pointers i.e. writePos and readPos
    - Move readPos (for loop) to non-zero element and swap with writePos.
    - Increase writePos by +1. In the end, all 0's will be at the end of the array

```java

class Solution {
    public void moveZeroes(int[] nums) {
        int writePos = 0;
        for (int readPos = 0; readPos < nums.length; readPos++) {
            if (nums[readPos] != 0) {
                int temp = nums[writePos];
                nums[writePos] = nums[readPos];
                nums[readPos] = temp;
                writePos++;
            }
        }
    }
}

```