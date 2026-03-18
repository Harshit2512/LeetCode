

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
    public List < Integer > boundaryOfBinaryTree(TreeNode root) {

        ArrayList < Integer > result = new ArrayList < Integer > ();
        if (!isLeaf(root)) {
            result.add(root.val);
        }

        addLeftBoundary(root, result);
        addLeaves(root, result);
        addRightBoundary(root, result);

        return result;
    }

    void addLeftBoundary(TreeNode root, ArrayList < Integer > result) {
        TreeNode curr = root.left;

        while (curr != null) {
            if (!isLeaf(curr)) result.add(curr.val);
            if (curr.left != null) curr = curr.left;
            else curr = curr.right;
        }
    }

    void addRightBoundary(TreeNode root, ArrayList < Integer > result) {
        TreeNode curr = root.right;

        ArrayList < Integer > temp = new ArrayList < Integer > ();

        while (curr != null) {
            if (!isLeaf(curr)) temp.add(curr.val);
            if (curr.right != null) curr = curr.right;
            else curr = curr.left;
        }

        for (int i = temp.size() - 1; i >= 0; i--) {
            result.add(temp.get(i));
        }
    }

    void addLeaves(TreeNode root, ArrayList < Integer > result) {
        if (isLeaf(root)) {
            result.add(root.val);
            return;
        }

        if (root.left != null) addLeaves(root.left, result);
        if (root.right != null) addLeaves(root.right, result);
    }


    boolean isLeaf(TreeNode root) {
        if (root.left == null && root.right == null) {
            return true;
        }

        return false;
    };
}

```

![Alternative Text](https://github.com/Harshit2512/LeetCode/blob/main/images/545_image1.jpg)