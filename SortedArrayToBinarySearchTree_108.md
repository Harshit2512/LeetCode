- **Time Complexity:** O(n), where n is the number of elements in the array. Each element is processed exactly once to construct the tree.
- **Space Complexity:** O(log n), which is the space complexity due to the recursion stack in the worst case of a balanced binary tree (height is log n).
- **Key Points:**
    - Divide and conquer approch: all element to mid will go to left sub tree and all elements to right will go in right sub tree
    - Recursive approach: Find mid, set left and right bounries from left and right children to parent node respectively and recurse the array
    - Iterative approach: Replace recursive calls with stack which store bounds of all left and right halves as we divide the array

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {

      // Base case
      if (nums == null || nums.length == 0)  return null;

     // Iterative approach

        // Stack<Bound> stack = new Stack<>();
        // int m = nums.length / 2;

        // TreeNode root = new TreeNode(nums[m]);
        // stack.push(new Bound(root, 0, m - 1, true));
        // stack.push(new Bound(root, m + 1, nums.length - 1, false));

        // while (!stack.isEmpty()) {
        //     Bound b = stack.pop();

        //     if (b.left > b.right) {
        //         continue;
        //     }

        //     int mid = b.left + (b.right - b.left) / 2;
        //     TreeNode node = new TreeNode(nums[mid]);

        //     if (b.isLeft) {
        //          b.parent.left = node;
        //     } else {
        //         b.parent.right = node;
        //     }

        //     stack.push(new Bound(node, b.left, mid - 1, true));
        //     stack.push(new Bound(node, mid + 1, b.right, false));
        // }

        // return root;

      // Recursive approach
      return buildTree(nums, 0, nums.length - 1);
    }

    private TreeNode buildTree(int[] nums, int left, int right) {

        // Base case for boundry check
        if (left > right) {
            return null; 
        }

        int mid = left + (right - left) / 2;

        // build a node from mid element
        TreeNode node = new TreeNode(nums[mid]);

        node.left = buildTree(nums, left, mid - 1); // left sub tree node from parent
        node.right = buildTree(nums, mid + 1, right); // right sub tree node from parent

        return node;
    }

    // private static class Bound {
    //     TreeNode parent;
    //     int left;
    //     int right;
    //     boolean isLeft;

    //     Bound(TreeNode node, int l, int r, boolean isLeft) {
    //         parent = node;
    //         left = l;
    //         right = r;
    //         isLeft = isLeft;
    //     }
    // } 
}
```