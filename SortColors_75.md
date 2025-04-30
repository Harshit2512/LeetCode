- **Time Complexity:** O(n), where n is the number of elements in the array. We perform a single linear scan of the array.
- **Space Complexity:** O(1), as we are using only constant extra space for the pointers. 
- **Key Points:**
    - One-pass Dutch National Flag Problem (Three Pointers)
    - low, mid and high pointers, if 0 then replace low with mid, if 1 then just increase mid and if 2 then replace high with mid

```java
class Solution {
    public void sortColors(int[] nums) {

        int low = 0, mid = 0;
        int high = nums.length - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
                // Swap mid and low
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                // Keep 1 as it is since moving 0 and 2
                mid++;
            } else {
                // Swap mid and high
                int temp = nums[high];
                nums[high] = nums[mid];
                nums[mid] = temp;
                // Don't increase mid bcz reevaluation required in case other than 2
                high--;
            }
        }
    }
}
```