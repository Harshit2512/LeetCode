- **Time Complexity:**  O(n) - Each node is visited once, and each node provides instantaneous information for further computations.
- **Space Complexity:** O(h) - The depth of the recursion stack, where h is the height of the tree, due to recursion.
- **Key Points:**
    - Approach: Optimized DFS with Return Values (Most Optimal)
    - Perform DFS on left and right subtree and calculate pair of value at each node in case not robbed or robbed ==> array [don't rob node, rob node]
    - If choose to rob the node then can't rob next connected node. so take array element val of not robbing the node
    - If choose to not to rob current node then decide robbing which node of subtree will maximize money and pick 0 or 1 element from  prev node pair
    - Result would be max of final pair (telling should we start robbing from root node or not)

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
    public int rob(TreeNode root) {
        int[] robResult = new int[2];
        robResult = dfs(root);
        return Math.max(robResult[0], robResult[1]);
    }

    private int[] dfs(TreeNode node) {

        if (node == null) {
            return new int[2];
        }

        // perform dfs and update array [don't rob node, rob node] for each node
        int[] left = dfs(node.left);
        int[] right = dfs(node.right);

        int[] res = new int[2];

        // update array [don't rob node, rob node] for selection of not robbing or robbing current node
        // element update when current node is not robbed
        // left[0] and left[1] selection comes based on what node robing can give max money. Same for right sub tree
        res[0] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);

        // if node is robbed then next node can't be robbed so take [0 -> don't rob node] of left and right
        res[1] = node.val + left[0] + right[0];

        return res;
    }
}
```