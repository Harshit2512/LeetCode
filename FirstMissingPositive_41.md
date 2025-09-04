- **Time Complexity:** O(n) - Each number is visited at most twice.
- **Space Complexity:** O(1) - In-place sorting without additional space.
- **Key Points:**
    - Approach: Cyclic Sort => Each positive number x (where 1 <= x <= n) should ideally be placed at index x - 1
    - Iterate through the array and swap numbers to their correct positions if they are within the valid range (1 to n)
    - Swap the number to their correct position. Numbers greater than n or less than 1 are ignored during placement
    - After sorting, iterate again to find the first index where the number is not equal to index + 1

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;

        // Iterate through the array and swap numbers to their correct positions if they are within the valid range (1 to n).
        for (int i = 0; i < n; i++) {
            // Swap the number to their correct position
            // Numbers greater than n or less than 1 are ignored during placement
            // Take the number at index i (x) and put it where it belongs (at index x-1).
            while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
                // Swap number x to correct position index (x-1)
                int temp = nums[nums[i] - 1];
                nums[nums[i] - 1] = nums[i];
                nums[i] = temp;
            }
        }

        // After sorting, iterate again to find the first index where the number is not equal to index + 1
        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }

        return n + 1;
    }
}
```