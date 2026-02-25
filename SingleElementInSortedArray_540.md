- **Time Complexity:** O(logN), binary search
- **Space Complexity:** O(1), no additional space
- **Approach: Binary Search**
    - Key words for clue : element appears exactly twice, except for one element (creates pair at (even, odd) indexes)
    - Start low = 1 and high = n - 1 to eliminate index out of bound error for extremes during comparision
    - If current mid element is diffrenet then its prev and next elements then it's the single element
    - If current index is odd, then if prev index element (even, odd) is same OR If current index is even, then if next index element (even, odd) is same means element is in   left half bcz all nums are in pair in left half, hence eliminate left half
    - If not then element is in right half, eliminate right half

```java

class Solution {
    public int singleNonDuplicate(int[] nums) {

        int n = nums.length;
        
        // Edge case - If array has only one element then it is single element
        if (n == 1) return nums[0];

        // Edge case for first index element, check it to avoid out of bound error in BS 
        if (nums[1] != nums[0]) {
            return nums[0];
        }

        // Edge case for last element, check it to avoid out of bound error in BS
        if (nums[n - 1] != nums[n - 2]) {
            return nums[n - 1];
        }

        // Start low = 1 and high = n - 1 to eliminate index out of bound error for extremes during comparision
        int low = 1;
        int high = n - 2;

        while (low <= high) {
            
            int mid = (low + high) / 2;

            // If current mid element is diffrenet then its prev and next elements then it's the single element
            if (nums[mid - 1] != nums[mid] && nums[mid] != nums[mid + 1]) return nums[mid];

            // For left half test
            // If current index is odd, then if prev index element (even, odd) is same OR
            // If current index is even, then if next index element (even, odd) is same
            // means element is in left half bcz all nums are in pair in left half, hence eliminate left half  
            if ((mid % 2 == 1 && nums[mid] == nums[mid - 1]) || 
                (mid % 2 == 0 && nums[mid] == nums[mid + 1])) {
                    // Element is in left half bcz all nums are in pair in left half, hence eliminate left half
                    low = mid + 1;
            } else {
                // Element is in right half, eleminate right half
                high = mid - 1;
            }
        }

        return -1;
    }
}

```