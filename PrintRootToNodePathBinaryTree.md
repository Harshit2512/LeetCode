- **Question** - Given input node, get all nodes in path from root uptil given node.
- **Approach:** In order traversal (root, left, right)
- **Time Complexity:** O(N)
- **Space Complexity:** O(H) - best and average case (If node is found on left half itself) O(N) - worst case (if node is found all the way right side of tree)

```java

public class Solution {

    private boolean getPath(TreeNode node, ArrayList<TreeNode> result, int x) {

        // If node is null, means reached to leaf node
        // node with given input not found untill now
        if (node == null) { 
            return false;
        }

        // If node has value then add into path
        result.add(node.val);

        // Check if node value is equal to input, if yes then return true
        // No need to iterate rest tree and true will be propogated all the way up
        if (node.val == x) {
            return true;
        }

        // If any of the left or right path is true then return true (Node found)
        if (getPath(node.left, result, x) || getPath(node.right, result, x)) {
            return true;
        }

        // Can't check condition like below bcz it will attempt to iterate other side even though one side already returned true
        // boolean left = getPath(node.left, result, x);
        // boolean right = getPath(node.right, result, x);

        // if (left || right) { return true};


        // backtrack step
        // if node with target value is not found until leaf then remove last added node from path and backtrack
        result.remove(result.size() - 1);
        return false;

    }

    public ArrayList<Integer> solve(TreeNode root, int input) {
        ArrayList<Integer> result = new ArrayList<>();

        // If given tree is null then return result
        if (root == null) return result;
        
        // Start iterating binart tree
        getPath(root, result, input);

        // Return result at the end
        return result;
    }
}




```