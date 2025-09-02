- **Time Complexity:** O(n) because it involves two passes over the array.
- **Space Complexity:** O(1) extra space apart from the output array.
- **Key Points:**
    - Single pass approach
    - Initialize the result array by computing the prefix (left) products.
    - Use a single variable right to iterate from the end of the array, updating the result by multiplying with right.
    - Update right in each iteration as you progress from right to left.

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        
        int n = nums.length;
        // Define array for result
        int[] result = new int[n];

        // Update result array as prefix products 
        result[0] = 1;

        for (int i = 1; i <  n; i++) {
            result[i] = result[i - 1] * nums[i - 1];  
        }

        // Use variable right to calculate suffix with directly calculating result
        int right = 1;

        for (int i = n - 1; i >= 0; i--) {
            result[i] = result[i] * right;
            // Update variable for suffix
            right = right * nums[i];
        }

        return result;
    }
}
```