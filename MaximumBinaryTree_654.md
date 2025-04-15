- **Time Complexity:** O(n^2) in the worst case where the array is sorted and each recursive call will scan through the array slice to find the max. However, in average cases, this is closer to O(n log n). Here O(n), to iterate n elements during sorting and O(log n), at each step problem reduces to half of size
- **Space Complexity:** O(n) to keep the recursion stack due to the depth of the recursion.
- **Key Points:**
    - Find the max element from array and divide array and conquer by doing recursion

```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return constructMaxBTree(nums, 0, nums.length);
    }

    private TreeNode constructMaxBTree(int[] nums, int left, int right) {

        // if sub array size is zero, meaning left and right index pointer at the same position 
        // then create null node there
        if (left == right) {
            return null;
        }

        int maxEleIndex = findMaxElementIndex(nums, left, right);

        // Create node for max element
        TreeNode root = new TreeNode(nums[maxEleIndex]);

        // iterate recursively for left and right subArray prefix from maximum element
        root.left = constructMaxBTree(nums, left, maxEleIndex); 
        root.right = constructMaxBTree(nums, maxEleIndex + 1, right); 

        return root;
    }

    private int findMaxElementIndex(int[] nums, int left, int right) {

        // Assume left most ele is maximum
        int maxIndex = left;

        for (int i = left + 1; i < right; i++) {
            // compare each current ele with maximum element index found so far
            if (nums[i] > nums[maxIndex]) maxIndex = i;
        }

        return maxIndex;
    }
}
```