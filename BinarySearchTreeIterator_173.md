- **Time Complexity:** 
    - Constructor: O(H), where H is the height of the tree, due to pushing nodes from the root to the leftmost leaf.
    - next(): Amortized O(1), each node pushed or popped exactly once.
    - hasNext(): O(1).
- **Space Complexity:** O(H), where H is the height of the tree, for the stack. This is optimal for very skewed trees.
- **Key Points:**
    - Use controlled stack-based recursion so that not all nodes pused to stack. Push only those nodes which appear on path of leftmose left node
    - Push all nodes on the way to leftmost leaf in left subtree
    - First popped node from stack is the next smallest node val according to in-order traversal fashion, also set up stack for current node's right subtree for next next() call
    - If stack is not empty then there is next node present

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
class BSTIterator {

    Stack<TreeNode> stack;

    public BSTIterator(TreeNode root) {
        
        // initialize stack to store all nodes on the way to leftmost leaf in left subtree
        stack = new Stack<TreeNode>();
        leftSubTreeTraversal(root);
    }

    private void leftSubTreeTraversal(TreeNode node) {

        // Push all left nodes to root into stack
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
    }
    
    public int next() {
        TreeNode nextSmallNode = stack.pop();

        // In case current node (i.e. nextSmallNode) has right child node and left subtree then set up stack for next next() call to return next smallest node val according to in-order retrival fasion
        if (nextSmallNode.right != null) {
            // push all left subtree nodes to stack
            leftSubTreeTraversal(nextSmallNode.right);
        }

        // return next smallest node value
        return nextSmallNode.val;        
    }
    
    public boolean hasNext() {
        // If stack is not empty then there exist next smallest node in tree
        return !stack.isEmpty();
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
 ```