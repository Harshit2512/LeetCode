- **Time Complexity:** O(N), since we only pass through each node once.
- **Space Complexity:** O(N), due to recursion call stack (worst case for skewed tree).
- **Key Points:**
    - Traverse left and right sub tree to their leaf node, which will give left and right side height
    - height of both sub trees give diameter, keep finding max diameter at each node level

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
    private int maxDiameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        calculateDiameterAndHeight(root);
        return maxDiameter;
    }

    private int calculateDiameterAndHeight(TreeNode node) {
        if (node == null) return 0;

        // traverse complete left and right subtree from current node, which will give left and right subtree height
        int leftHeight = calculateDiameterAndHeight(node.left);
        int rightHeight = calculateDiameterAndHeight(node.right);
        
        // left height + right height gives diameter
        int diameterThroughNode = leftHeight + rightHeight;

        maxDiameter = Math.max(maxDiameter, diameterThroughNode);

        // max height of the tree
        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```