- **Time Complexity:** O(log N), binary search
- **Space Complexity:** O(1), no additional space
- **Approach:** Binary Search (finding element op in kind of sorted array)
    - Handle overflow error for first and last elements, Both side are negetive infinitive (going downward), nums[0] > nums[1] and nums[n - 1] > nums[n - 2]
    - Check if mid is the peak by checking nums[mid - 1] < nums[mid] > nums[mid + 1]
    - Check if peak is in right half => eliminate left half
    - If not, eliminate right half (handles both peak being in the left half and multiple peaks scenarios)

```java

class Solution {
    public int findPeakElement(int[] nums) {
        int n = nums.length;
        // If array has only one element
        if (n == 1) return 0;

        // Handle overflow error for first and last elements
        // Both side are negetive infinitive (going downward), nums[0] > nums[1] and (nums[n - 1] > nums[n - 2]
        if (nums[0] > nums[1]) return  0;

        if (nums[n - 1] > nums[n - 2]) return n - 1;

        int low = 1, high = n - 2;

        while (low <= high) {

            int mid = (low + high) / 2;

            // Check if mid is the peak by checking nums[mid - 1] < nums[mid] > nums[mid + 1]
            if (nums[mid - 1] < nums[mid] && nums[mid] > nums[mid + 1]) {
                return mid;
            }

            // Check if peak is in right half => eliminate left half
            if (nums[mid - 1] < nums[mid]) {
                low = mid + 1;
            } else {
                // If not, eliminate right half (handles both peak being in the left half and multiple peaks scenarios)
                high = mid - 1;
            }
        }

        return -1;
    }
}

```