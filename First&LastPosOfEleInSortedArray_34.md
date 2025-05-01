- **Time Complexity:** O(log n) if elements are scattered, but potentially O(n) if all elements are the same and span both sections.
- **Space Complexity:** O(1), no extra space required
- **Key Points:**
    - Keep finding the left/right half where target element could be found
    - Once target element is found, from that point, stretch the windows both left and right until target element is found

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int start = -1, end = -1;

        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left)/2;
            if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                // Target element is found
                start = mid;
                end = mid;

                // Stretch window left side till target is found
                while (start - 1 >= 0 && nums[start - 1] == target) {
                    start--;
                } 

                // Stretch window right side till target is found
                while (end + 1 < nums.length && nums[end + 1] == target) {
                    end++;
                }

                return new int[] {start, end};
            }
        }
        return new int[] {start, end}; 
    }
}
```