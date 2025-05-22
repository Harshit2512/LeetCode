- **Time Complexity:** O(N), where N is the number of nodes. We avoid repeated scanning of inorder by using HashMap.
- **Space Complexity:** O(N), for the recursion call stack and the HashMap.
- **Key Points:**
    - Identify the root from the preorder list. El at index 0 is always the root el in preorder sub list
    - Find the index of this root in the inorder list.
    - Split the inorder list into left and right (halves) subtrees.
    - Recursively build the left and right subtrees by passing sub array ranges in preorder and inorder arrays

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inOrderMap = new HashMap<>();
        
        // build hashmap for inorder array to perform constant time search of root node index
        for (int i = 0; i < inorder.length; i++) {
            inOrderMap.put(inorder[i], i);
        }

        return buildTreeHelper(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1, inOrderMap);
    }

    private TreeNode buildTreeHelper(int[] preorder, int preorderStart, int preorderEnd, int[] inorder, int inorderStart, int inorderEnd, Map<Integer, Integer> inOrderMap) {

        // Base case: no element left to construct treen anymore
        if (preorderStart > preorderEnd || inorderStart > inorderEnd) return null;

        // get root node for each sub tree from preorder array
        // For preorder, root is located at the first index of the array (order: root, left, right)
        TreeNode root = new TreeNode(preorder[preorderStart]);

        // Find the index of the above root from inorder array
        // for given mid index, all element left to the mid will be part of left subtree and all elements right of the mid will be part of right subtree
        int mid = inOrderMap.get(root.val);
        int subArrSize = mid - inorderStart;

        // use subArrSize to decide left and right subtree halves range in preorder array
        // recursive construction of left and right subtrees
        root.left = buildTreeHelper(preorder, preorderStart + 1, preorderStart + subArrSize, inorder, inorderStart, mid - 1, inOrderMap);
        root.right = buildTreeHelper(preorder, preorderStart + subArrSize + 1, preorderEnd, inorder, mid + 1, inorderEnd, inOrderMap);

        return root;
    } 
}
```