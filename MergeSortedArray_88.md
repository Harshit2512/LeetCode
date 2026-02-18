- **Time Complexity:** O(m + n), as we iterate through both arrays once.
- **Space Complexity:** O(m + n), due to the use of an additional array.
- **Apparoach:**
    - Two Pointer technique (Merge part of merge sort algorithm)
    - Initialize three pointers: p1 for nums1, p2 for nums2, and p for the new array.
    - Compare elements pointed by p1 and p2, and place the smaller one in the new array.
    - If any elements are left in nums1 or nums2, append them to the end of the new array.
    - Copy the new array back into nums1.

```java

public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // New array to store merged result
        int[] sorted = new int[m + n];
        // Pointers for nums1, nums2, and sorted array
        int p1 = 0, p2 = 0, p = 0;
        
        // Compare and merge
        while (p1 < m && p2 < n) {
            if (nums1[p1] <= nums2[p2]) {
                sorted[p++] = nums1[p1++];
            } else {
                sorted[p++] = nums2[p2++];
            }
        }
        
        // Append remaining elements
        while (p1 < m) {
            sorted[p++] = nums1[p1++];
        }
        while (p2 < n) {
            sorted[p++] = nums2[p2++];
        }
        
        // Copy sorted array back to nums1
        System.arraycopy(sorted, 0, nums1, 0, m + n);
    }
}

```