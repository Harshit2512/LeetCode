- **Time Complexity:** O(log n), binary search divides the problem in the half
- **Space Complaxity:** O(1), no extra space needed
- **Key Points:**
    - Determine which half is sorted respective to mid point and perform search in that part
    - If in assumed part, given criteria is not met then target could be in other half

```java
class Solution {
    public int search(int[] nums, int target) {
       int left = 0; 
       int right = nums.length - 1;

       while (left <= right) {

        int mid = left + (right - left)/2;
        if (nums[mid] == target) {
            return mid;
        }

        if (nums[left] <= nums[mid]) { // Left half is sorted
            if (nums[left] <= target && target < nums[mid]) { 
                // validate assumption that target being in left half by checking given condition
                right = mid - 1;
            } else {
                // given condition is not validated then assumption is not correct and target could be in right half
                left = mid + 1;
            }
        } else { // Right half is sorted 
            if (nums[mid] < target && target <= nums[right]) {
                // validate assumption that target being in right half by checking given condition
                left = mid + 1;
            } else {
                // given condition is not validated then assumption is not correct and target could be in left half
                right = mid - 1;
            }
        }

       }

        return -1;

    }
}
```