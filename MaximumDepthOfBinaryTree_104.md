- **Approach: Recursive**
    - Recursively iterate left and right halfs and add 1 in max of left and right half depth (1 + Math.max(lh, rh))
- **Approach: Iterating (BFS using queue)**
    - Add root in queue
    - Iterate queue untill empty. Each time take snapshot (size of the queue)
    - Take out each node and add each node's left and right nodes
    - After completing iterating snapshot each time, increase level

```java

class Solution {
    public int maxDepth(TreeNode root) {
        // Recursive approach
        // Time Complexity: O(N), all nodes must be traversed once
        // Space Complexity: O(N), stack space - in worst case when tree is linear

        // If reached to leaf node then return 0
        if (root == null) return 0;
        
        // Recursively iterate left half of current node
        int lh = maxDepth(root.left);

        // Recursively iterate right half of current node
        int rh = maxDepth(root.right);

        // When left and right half of current node iterated, take the max of it (height uptil this node)
        // Recursively calculate height at each node and propogate up until main root
        return 1 + Math.max(lh, rh);
    }


    // public int maxDepth(TreeNode root) {
    //     // Iterative approach - BFS using queue
    //     // Time Complexity: O(N), all nodes must be traversed once
    //     // Space Complexity: O(N), queue space
        
    //     // If tree is empty, return 0;
    //     if (root == null) return 0;

    //     int level = 0;
    //     Queue<TreeNode> queue = new LinkedList<TreeNode>();
        
    //     queue.add(root);

    //     while (!queue.isEmpty()) {

    //         // Take snapshot of queue, which will give current size of queue
    //         int size = queue.size();

    //         // Remove nodes and add node's left and right children
    //         for (int i = 0; i < size; i++) {
    //             TreeNode node = queue.remove();
    //             if (node.left != null) {
    //                 queue.add(node.left);
    //             }

    //             if (node.right != null) {
    //                 queue.add(node.right);
    //             }
    //         }

    //         // After completing iterating snapshot each time, increase level
    //         level++;
    //     }
        
    //     return level;
    // }
}

```