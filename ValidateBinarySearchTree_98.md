- **Time Complexity:** O(N) where N is the number of nodes in the BST because each node is visited exactly once.
- **Space Complexity:** O(N) for the recursion stack or using stack DS.
- **Key Points:**
    - **Recursive approach:**
        - Valid condition: current node value should be greater than last seen node value. If not then not a valid BST
        - Traverse left and right su tree recursively and validate, if valid the asign node value as last seen
    - **Iterative approach:**
        - using stack and while loop replace recusion and make it iterative approach
        - first Visit all nodes in left sub tree and push to stack
        - get the node from stack and check for validation. if not valid then return false;
        - visit all right nodes in sub tree

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
    //private Integer lastSeen = null;
    public boolean isValidBST(TreeNode root) {

        // Iterative approach
        Stack<TreeNode> stack = new Stack<>();
        Integer lastSeen = null;
        TreeNode current = root;

        while (!stack.isEmpty() || current != null) {

            // visit all nodes from left sub tree and reach to las left node
            while (current != null) {
                stack.push(current);
                current = current.left;
            }

            current = stack.pop();

            // validate condition
            if (lastSeen != null && current.val <= lastSeen) {
                return false;
            }
            lastSeen = current.val;

            // visit right node in sub tree
            current = current.right;
        }

        return true;

        //return inOrderTraversal(root);
    }

    // private boolean inOrderTraversal(TreeNode node) {

    //     // handles the case where root is null or last node in left or right sub tree is null (end of the sub tree)
    //     if (node == null) {
    //         return true;
    //     }

    //     // visit recursively left sub tree, if left sub tree node doesn't follow valid condition then return false (not a valid BST)
    //     if (!inOrderTraversal(node.left)) {
    //         return false;
    //     }

    //     // BST Validation condition
    //     // lastSeen can be null for very first node visitation, in this case continue and assign current node as lastSeen node
    //     // If current node value is less than last seen node value then not a valid BST
    //     if (lastSeen != null && node.val <= lastSeen) {
    //         return false;
    //     }

    //     // assign current node as ast seen and continue visiting right sub tree 
    //     lastSeen = node.val;

    //     // visit recursively right sub tree
    //     return inOrderTraversal(node.right);
    // }
}
```