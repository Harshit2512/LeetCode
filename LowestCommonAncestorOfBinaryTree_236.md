- **Time Complexity:** O(N), where N is the number of nodes in the binary tree. Each node is visited once.
- **Space Complexity:** O(N), recursive call stack
- **Key Points:**
    - Keep visiting left subtree and return value (null if not eq to targets or return node if matches any of targets)
    - Keep visiting right subtree and return value (null if not eq to targets or return node if matches any of targets)
    - At point where node's left and right both are not null, return that node which is LCA

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        
        // if left or right child is null or node matches target then return that node
        if (root == null || root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        // If left and right both are note null then that ode is LCA
        if (left != null && right != null) {
            return root;
        }

        // return child node which is not null
        return left != null ? left : right;
    }
}
```