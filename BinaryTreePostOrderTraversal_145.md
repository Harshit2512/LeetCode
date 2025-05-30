- **Time Complexity:** O(N), since each node is visited exactly once.
- **Space Complexity:** O(N) in the worst case, elements in the stack might be as large as the height of the tree.
- **Key Points:**
    - Post order : left, right and then root
    - Iterative approach: Use stack
        - First visit left sub tree to it's depth
        - Peek the node and if right child node is not null then visit left sub tree of right child.. in this way all right child of sub tree wil be processed as root of next sub tree
        - Pop root node and add it's value to result

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
    public List<Integer> postorderTraversal(TreeNode root) {

        List<Integer> result = new ArrayList<>();

        // Recursive approach
        // postorder(root, result);
        // return result;

        // Iterative approach
        Stack<TreeNode> stack = new Stack<>();
        TreeNode current = root;
        TreeNode lastVisited = null;

        while (!stack.isEmpty() || current != null) {

            if (current != null) {
                stack.push(current);
                current = current.left; // explore left sub tree depth
            } else {
                TreeNode peekNode = stack.peek();
                if (peekNode.right != null && lastVisited != peekNode.right) {
                    current = peekNode.right; // explore right sub tree depth
                } else {
                    result.add(peekNode.val); // visit the root node and add value to result
                    lastVisited = stack.pop();
                }
            }
        }

        return result;
    }
    
    // private void postorder(TreeNode node, List<Integer> result) {
    //     if (node == null) return; // Base case: If the node is null, return
    //     postorder(node.left, result);  // Recursively visit left subtree
    //     postorder(node.right, result); // Recursively visit right subtree
    //     result.add(node.val);          // Add node's value after children
    // }
}
```