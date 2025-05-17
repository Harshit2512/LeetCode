- **Time Complexity:** O(N), each node in the tree is visited once
- **Space Complexity:** O(N), call stack space for iteration of each node in the tree
- **Key Points:**
    - Keep track of tree depth (level) to know if node is at same level and needs to be added in same sub list
    - Recurse the tree for node's left and right child

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        List<List<Integer>> result = new ArrayList<>();
        levelOrderTraversal(root, 0, result);
        return result;
    }

    private void levelOrderTraversal(TreeNode node, int depth, List<List<Integer>> result) {
        
        // Base case: if node is null then continue with other call in call stack
        if (node == null) { 
            return;
        }

        // condition to decide if node is at the which and same level as other prev processed nodes
        if (depth == result.size()) {
            result.add(new ArrayList<>());
        }

        result.get(depth).add(node.val);
        levelOrderTraversal(node.left, depth + 1, result); // next level traversal for left node
        levelOrderTraversal(node.right, depth + 1, result); // next level traversal for right node
        
    }
}
```