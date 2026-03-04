- **Time Complexity: O(N)**
- **Space Complexity:** (N), recursive call stack
- **Approach: Extension of finding maximun depth (height) of the tree by recursive way**
    - Find height of left and right tree from current node recursively
    - If left or right sub tree height is -1, means not balanced tree
    - If Absolute difference is greater than 1 then return -1 (not balanced tree)
    - Take the max of left and right sub tree and increase by 1

```java 

class Solution {
    public boolean isBalanced(TreeNode root) {
        // If return -1 that means tree is not balanced
        return depth(root) != -1;
    }

    public int depth(TreeNode root) {

        // If tree has no node or reached to leaf node then return height as 0
        if (root == null ) return 0;

        // Find height of left and right tree from current node recursively
        int lh = depth(root.left);
        int rh = depth(root.right);

        // If left or right sub tree height is -1, means not balanced tree
        if (lh == -1 || rh == -1) return -1;

        // If Absolute difference is greater than 1 then return -1 (not balanced tree)
        if (Math.abs(rh - lh) > 1) return -1;

        // Take the max of left and right sub tree and increase by 1
        return 1 + Math.max(lh, rh);
    }
} 

```