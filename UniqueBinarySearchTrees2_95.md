
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
    public List<TreeNode> generateTrees(int n) {
        
        // Base case: If input n = 0 then no tree can be formed. So return empty tree
        if (n == 0) {
            return new ArrayList<TreeNode>();
        }

        // List<TreeNode> memo = new ArrayList[n + 1][n + 1];
        return genTree(1, n, new ArrayList[n + 1][n + 1]);
    }

     private List<TreeNode> genTree(int start, int end, List<TreeNode>[][] memo) {

        List<TreeNode> trees = new ArrayList<>();
        
        if (start > end) {
            // why null: create null node. If return empty then below nested second for loop for right sub trees won't be ever executed for left node
            trees.add(null);
            return trees;
        }

        // If for given range, sub trees are already computed then return from memo
        if (memo[start][end] != null) {
            return memo[start][end];
        }


        // For given range, consider each node as root and create left and right subtrees
        for (int i = start; i <= end; i++) {
            // for each node as root node, create all possible left and right sub trees
            List<TreeNode> leftSubTrees = genTree(start, i - 1, memo);
            List<TreeNode> rightSubTrees = genTree(i + 1, end, memo);

            for (TreeNode left : leftSubTrees) {
                for (TreeNode right : rightSubTrees) {
                    // Create root node for current node
                    TreeNode currentTree = new TreeNode(i);
                    currentTree.left = left;
                    currentTree.right = right;
                    trees.add(currentTree);
                }
            }
        }

        // With given range, add all created possible subtree in memo
        memo[start][end] = trees;
        return trees;

    }
}
```