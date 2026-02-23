**Time Complexity:** O(logN), best and avg case
                  O(n/2) + O(logN), if elements are high and many duplicates and need to shrink window at huge extent
**Space Complexity:** O(1), no additional space
**Approach:** Striver
    - https://www.youtube.com/watch?v=w2G2W8l__pc&t=4s
    - Extension of Search in Rotated Sorted Array 1 problem
    - Binary search with window shrink when low and high are same and which half to remove is unconclusive
    - Shrink dow window until low != high

```java

class Solution {
    public boolean search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low)/2;
            // Base case:
            if (nums[mid] == target) {
                return true;
            }

            // Condition not satisfied due to duplicate (low == high) that makes which half to remove unconclusive
            // Further shrink dow window until don't have low and high the same 
            if (nums[low] == nums[mid] && nums[mid] == nums[high])  {
                low++;
                high--;
                continue;
            }

            // Check if left half is sorted
            if (nums[low] <= nums[mid]) {
                // Left half is sorted then check if target present in left half
                // If present in left half then eliminate right half else eliminate left half
                if (nums[low] <= target && target <= nums[mid]) {
                    high = mid -1;
                } else {
                    low = mid + 1;
                }
            } else { // Right half is sorted
                // Right half is sorted then check if target present in right half
                // If present in right half then eliminate left half else eliminate right half
                if (nums[mid] <= target && target <= nums[high]) {
                    low = mid + 1;
                } else {
                   high = mid - 1;
                }
            }

        }

        // If search space exhausted then return target not present and return false
        return false;
    }
}

```