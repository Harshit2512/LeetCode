- **Time Complexity:** O(log n), at each step problem space is divided into half (Binary Search)
- **Space Complexity:** O(1), no extra space
- **Key Points:**
    - Find mid, if right is less than mis then right half is rotated and min ele could be right side, set left to mid + 1 to iterate right half and vice versa

```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;

        if (nums.length == 1) return nums[0];

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] > nums[right]) { // min could be right side
                left = mid + 1; // move left to iterate in right half
            } else {
                right = mid; // move right to iterate in left half
            }
        }

        return nums[left];
    }
}
```