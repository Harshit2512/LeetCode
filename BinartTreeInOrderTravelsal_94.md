- **Time Complexity:** O(n), where n is the number of nodes in the tree. Each node is processed exactly once.
- **Space Complexity:** O(n) in the worst case (for a completely skewed tree) and O(log n) for a balanced tree.
- **Key Points:**
    - Recursive approach: recursively iterate left sub tree then visit root node and then recursively visit right sub tree
    - Iterative approach: Use stack for iteration
        - Take the root node and visit all left sub tree (until extreme left node)
        - Then pop the node visit and add to result
        - add root in the result and then iterate right sub tree

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
    public List<Integer> inorderTraversal(TreeNode root) {
        
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        // Recursive approach:
        //inorderTraversalHelper(root, result);

        // Iterative approach
        TreeNode current = root;

        while (!stack.isEmpty() || current != null) {
            
            // Iterate left node and reach to extrem left node 
            while (current != null) {
                stack.push(current);
                current = current.left;
            }
            // current is null at this point
            current = stack.pop();
            // visit the node and add to result
            result.add(current.val);
            // Now visit right sub tree
            current = current.right;
        }
        return result;
    }

    // private void inorderTraversalHelper(TreeNode node, List<Integer> result) {
    //     if (node != null) {
    //         // Iterate left subtree
    //         inorderTraversalHelper(node.left, result);
    //         // add root node
    //         result.add(node.val);
    //         // Iterate right subtree
    //         inorderTraversalHelper(node.right, result);
    //     }
    // }
}
```