- **Time Complexity:** O(logN), Binary search where N is size of array
- **Space Complexity:** O(1), no additional space
- **Approach:** Binary search with duplicates (Extension of find minimum from rotated sorted array with uniques) - Striver
    - Find mid and check if both half is sorted, If low and high both are same (due to duplicate, then can't conclude which half is sorted). Shrink the window until nums[low] != nums[high]
    - Once sorted half is found, take min from sorted half before removing it
    - Perform BS in unsorted half and repeat process

```java

class Solution {
    public int findMin(int[] nums) {
        int min = Integer.MAX_VALUE;
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = (low + high)/2;
            min = Math.min(nums[mid], min);
            
            // Additional condition to handle duplicates
            // if low and high both are same (due to duplicate, then can't conclude which half is sorted). Shrink the window until nums[low] != nums[high] 
            if (nums[low] == nums[mid] && nums[mid] == nums[high]) {
                low++;
                high--;
                continue;
            }

            // check if left half is sorted, if sorted then take min and remove left half
            if (nums[low] <= nums[mid]) {
                min = Math.min(nums[low], min);
                low = mid + 1;
            } else {
            // right half is sorted
                min = Math.min(nums[mid], min);
                high = mid - 1;
           }
        }

        return min;
    }
}

```