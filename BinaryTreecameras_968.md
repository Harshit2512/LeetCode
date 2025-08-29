- **Time complexity:** O(n) each node is visited once.
- **Space complexity:** O(h) recursion stack (h = tree height), worst-case O(n) for skewed tree.
- **Key Points:**
    - (word doc) Approach: Geedy DFS -> Why Greedy? Leaf node enforces parent node to place camera to be covered
    - Leaves return 0. Parents of leaves get forced to place cameras. Higher nodes only place cameras if absolutely necessary.
    - DFS to reach until last node from left and right subtree
    - If children (or leaf nodes) are not covered, then parent must cover them. So place camera at this node
    - If any of the child has camera, then current node is already covered
    - If Both children are covered but none has a camera, then current node is not covered -> return 0

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

// 0 = NOT covered (this node needs its parent to place a camera),
// 1 = HAS CAMERA (we placed a camera at this node),
// 2 = COVERED (no camera here, but one of its children has a camera).

class Solution {
    int cameras = 0;

    public int minCameraCover(TreeNode root) {
        
        // Edge case-1 -> If single node tree then leaf return 0, hence this node requires camera to monitor itself 
        if (dfs(root) == 0) {
            cameras++;
        }
        return cameras;
    }

    private int dfs(TreeNode node) {
        // Base case + edge case
        // If node is null (last nodes in tree), consider them covered so that leaf nodes can emit 0 (uncovered)
        if (node == null) {
            return 2;
        }

        // DFS to reach until last node from left and right subtree
        int left = dfs(node.left);
        int right = dfs(node.right);

        // If children (or leaf nodes) are not covered, then parent must cover them. So place camera at this node
        if (left == 0 || right == 0) {
            cameras++;
            return 1;
        }

        // If any of the child has camera, then this node is already covered
        if (left == 1 || right == 1) {
            return 2;
        }

        // If node is not covered by any means then return 0;
        // Both children are covered but none has a camera -> this node is not covered
        return 0;

    }
}
```