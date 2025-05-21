- **Time Complexity:** O(n), iterate each node once and calculate prefix sum and find valid path count in same iteration
- **Space Complexity:** O(n), for the prefix sum store in hashmap and recursion stack in worst case
- **Key Points:**
    - Find running sum at each current node, see if prefixSum map has diff of runnning sum and target sum (means that diff val holding node was previously iterated in the path)
    - If diff present in map, increase path count 
    - at last, backtrack to iterate other half of the sub tree

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
    public int pathSum(TreeNode root, int targetSum) {
        Map<Long, Integer> prefixSumCount = new HashMap<>();
        prefixSumCount.put(0L, 1);
        return findPathCount(root, 0, targetSum, prefixSumCount); 
    }

    private int findPathCount(TreeNode node, long runningSum, int targetSum, Map<Long, Integer> prefixSumCount) {

        if (node == null) return 0;

        // current sum from root to current node
        runningSum += node.val;

        int pathCountsToCurrent = prefixSumCount.getOrDefault((runningSum - targetSum), 0);

        // update map for prefix sum current running sum 
        prefixSumCount.put(runningSum, prefixSumCount.getOrDefault(runningSum, 0) + 1);

        // recurse for left and right child nodes and find total no of paths
        pathCountsToCurrent = pathCountsToCurrent + findPathCount(node.left, runningSum, targetSum, prefixSumCount) + findPathCount(node.right, runningSum, targetSum, prefixSumCount);

        // reduce current running sum count to backtrack for other half of the tree/subtree
        // KP: backtrack is required to calculate for paths (top to bottom) in three and not sub trees
         prefixSumCount.put(runningSum, prefixSumCount.getOrDefault(runningSum, 0) - 1);

         return pathCountsToCurrent;

    }
}
```