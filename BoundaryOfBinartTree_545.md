- **Time Complexity:** O(H) -> left height + O(H) -> right height + O(W) -> leaf nodes ~= O(N)
- **Space Complexity:** O(N)
- **Apporach:**
    - Interate all the way left nodes until leaf found. Add node to list only if not leaf node 
    - Iterate leaf nodes only and add in list
    - Interate all the way right nodes until leaf found. Add nodes in temp list and get them in reverse order. Add node to list only if not leaf node
    - Premium question asked at multiple good companies

```java

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

        // Why 5 was not added? root node 4 is leaf node and its left and right are null. That's break while loop
        // Iterate all left nodes until leaf node not found. Add node to list only if not leaf node 
        while (curr != null) {
            if (!isLeaf(curr)) result.add(curr.val);
            if (curr.left != null) curr = curr.left;
            else curr = curr.right;
        }
    }

    // Iterate all right nodes until leaf node not found. Add node to list only if not leaf node
    // Add node values in temp list and get them in reverse order
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

    // Keep moving down until leaf nodes are found. Add in list only if leaf nodes
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