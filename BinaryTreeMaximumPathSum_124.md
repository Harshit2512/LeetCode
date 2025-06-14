- **Time Complexity:** O(N) since each node is processed exactly once.
- **Space Complexity:** O(H) where H is the height of the tree for the recursion stack.
- **Key Points:**
    - For current node, return max sum of either left or right child and calculate path sum for current node considering it's children with max path sum

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

    int max_path_sum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        pathSum(root);
        return max_path_sum;
    }

    private int pathSum(TreeNode node) {

        // if node is null then int to be added in sum is 0
        if (node == null) return 0;

        // if left/right path sum is less than 0 then we don't want to add in sum so return 0 or if left/right sum is positive then return it
        int left = Math.max(0, pathSum(node.left));
        int right = Math.max(0, pathSum(node.right));

        // calculate path sum for current node considering it's children with max path sum
        max_path_sum = Math.max(max_path_sum, left + right + node.val);

        // for current node, return max sum of either left or right child
        return node.val + Math.max(left, right);
    }
}
```