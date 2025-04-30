- **Time Complexity:** O(log N), N is the number of elements in the array. Binary search divide problem space into half at each step. hence logarithmic time complexity
- **Space Compelexity:** O(1), no extra space needed
- **Key Points:**
    - Find mid point and check in which half could target lie by comparing with mid
    - Move left or right pointers to divide space into half

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        
        int left = 0, right = nums.length - 1;    

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return left;
    }
}
```