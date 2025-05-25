- **Time Complexity:** O(N), where N is the number of nodes in the tree. In the worst case, we visit each node once.
- **Space Complexity:** O(H), where H is the height of the tree. This accounts for the recursive stack space.
- **Key Points:**
    - **Recursive approach:**
        - Traverse all nodes in left sub tree until extreme left node
        - Initialize count var and upon each node visited increase count, then compare count with given k, if count = k mean found the kth node
    - **Iterative approach:**
        - Use stack and push all nodes in left sub tree until extreme left node
        - Once left sub tree nodes are visited, pop them and decrease k on eack pop, if k = 0 then found the kth smallest 

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

    // private int count = 0;
    private int result = -1;

    public int kthSmallest(TreeNode root, int k) {

        // Iterative approach
        Stack<TreeNode> stack = new Stack<>();
        TreeNode current = root;

        while (!stack.isEmpty() || current != null) {

            // traverse left sub tree node until extreme left node
            while (current != null) {
                stack.push(current);
                current = current.left;
            }

            current = stack.pop();
            k--;

            if (k == 0) {
                result = current.val;
                return result;
            }

            current = current.right;
        }

        // Recusive approach
        // findKthSmallest(root, k);
        return result;
    }

    // private void findKthSmallest(TreeNode node, int k) {

    //     if (node == null) {
    //         return;
    //     }

    //     // Traverse left sub tree
    //     findKthSmallest(node.left, k);

    //     // increase count upon node visited and check count against given k
    //     count++;
    //     if (count == k) {
    //         result = node.val;
    //         return;
    //     }

    //     // Traverse right sub tree
    //     findKthSmallest(node.right, k);
    // }
}
```