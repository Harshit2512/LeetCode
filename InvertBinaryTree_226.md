- **Time Complexity:** O(n), Each node is visited once.
- **Space Complexity:** O(n), In the worst case, the queue will hold all the nodes in a level of the tree.
- **Key Points:**
    - Iterative approach using Queue (BFS) - level order traversal
    - Iterate root and swap it's children and then traverse sub tree (next level) of each child and put node in queue

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
    public TreeNode invertTree(TreeNode root) {
               
        if (root == null) return root;

        // Recursive approach
        // TreeNode left = invertTree(root.left);
        // TreeNode right = invertTree(root.right);

        // root.left = right;
        // root.right = left;

        // return root;

        // Iterative approach with BFS technique using queue

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            TreeNode current = queue.poll();

            // swap the children of root
            TreeNode temp = current.left;
            current.left = current.right;
            current.right = temp;

            // iterate sub tree (next level) of root
            if (current.left != null) {
                queue.offer(current.left);
            }

            if (current.right != null) {
                queue.offer(current.right);
            }
        }

        return root;
    }
}
```