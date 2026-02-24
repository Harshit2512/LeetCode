- **Time Complexity:** O(log n), at each step problem space is divided into half (Binary Search)
- **Space Complexity:** O(1), no extra space
- **Approach:** Binary search with uniques - Striver
    - Find mid and check which half is sorted
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