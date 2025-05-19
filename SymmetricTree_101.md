- **Time Complexity:** O(n), need to iterate all n nodes in the tree
- **Space Complexity:** O(n), where n is the number of nodes in the queue at any level (widest point of the tree). For a perfectly balanced tree, this would be approximately h/2 nodes, or n/2/3 in the worst case.
**Key Points:**
    - This is pre order tree traversal
    - For recursive approach, swap the left and right child of parent t1 and t2 nodes to check mirror

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
    public boolean isSymmetric(TreeNode root) {
        
        // Base case \
        if (root == null) return true; 

        // Iterative approach

        // Queue<TreeNode> queue = new LinkedList<>();
        // queue.add(root.left);
        // queue.add(root.right);

        // while (!queue.isEmpty()) {
        //     TreeNode t1 = queue.poll();
        //     TreeNode t2 = queue.poll();

        //     Since using Queue and passing left and right child nodes reverse roles, child could be null, If null then continue while loop, don't return false
        //     if (t1 == null && t2 == null) continue; 

        //     if (t1 == null || t2 == null || t1.val != t2.val) return false;

        //     queue.add(t1.left);
        //     queue.add(t2.right);
        //     queue.add(t1.right);
        //     queue.add(t2.left);
        // }

        // return true;

        //Recusrvie approach
        return isMirror(root.left, root.right);
    }

    private boolean isMirror(TreeNode left, TreeNode right) {
        
        TreeNode t1 = left;
        TreeNode t2 = right;
        // If both children are null (not present), then it's symmetrical (return true)
        if (t1 == null && t2 == null) return true;

        // If any of the child is null, it's not symmetrical
        if (t1 == null || t2 == null) return false;

        // Check if values are same and also recurse on chidren by swapping roles
        return (t1.val == t2.val) && isMirror(t1.left, t2.right) && isMirror(t1.right, t2.left);
    }
}
```