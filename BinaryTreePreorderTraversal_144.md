- **Time Complexity:** O(n), since each node is processed (visited and added to the result list) once.
- **Space Complexity:** O(n), in the worst case, due to the stack holding all nodes (in the case of a skewed tree). In the best case of a balanced tree, it's O(log n).
- **Key Points:**
    - Preorder Traversal: root, left subtree of current node, then right subtree of current node
    - Use stack for iterative approach, and push right child first to get right sub tree iterated before left subtree

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
    public List<Integer> preorderTraversal(TreeNode root) {
               
        List<Integer> result = new ArrayList<>();

        // Recursive approach
        // preOrderTraversalDfs(root, result);

        // Iterative approach : using stack DS

        if (root == null) {
            return result;
        }

        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode current = stack.pop();

            // push right child first for preorder traversal as stack follows first in last out
            if (current.right != null) {
                stack.push(current.right);
            }
            if (current.left != null) {
                stack.push(current.left);
            }
            result.add(current.val);
        }

        return result;
    }

    // private void preOrderTraversalDfs(TreeNode node, List<Integer> result) {
    //     // Base case: if node is null then return (i.e. continue with next call on call stack)
    //     if (node == null) {
    //             return;
    //     }
    //     result.add(node.val);
    //     preOrderTraversalDfs(node.left, result);
    //     preOrderTraversalDfs(node.right, result);
    // }
}
```