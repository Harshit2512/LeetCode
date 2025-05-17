- **Time Complexity:** O(N), need to iterate all nodes in the tree once
- **Space Complexity:** O(H), height of the tree for recursive call stack
- **Key Points:**
    - Recurse with the right child first to always have the most right child
    - Compare depth with result size to see if new tree level, if yes the add that node in the list

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        mostRightNode(0, root, result);
        return result;
    }

    private void mostRightNode(int depth, TreeNode node, List<Integer> result) {

        // Base case: if node is null then return
        if (node == null) {
            return;
        }

        // Check if new depth level, if new level then add node val to list and this will be the right mode node as right child node is passed first in recursive call
        if (depth == result.size()) {
            result.add(node.val);
        }

        // recurse right child node first to get the most right node all the time at same level 
        mostRightNode(depth + 1, node.right, result);
        // if right child from right side tree is null then right child from left side tree will be seen
        mostRightNode(depth + 1, node.left, result);
    }
}
```