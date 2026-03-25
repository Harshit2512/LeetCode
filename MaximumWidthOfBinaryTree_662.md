- **Time Complexity:** O(N), no of nodes in tree
- **Space Complexity:** O(N), Queue space for no of nodes in tree
- **Approach:** SV - Level order traversal using queue and index diff between last and first nodes in level
    - Maintain the index for all nodes (left = (2 * i) + 1 and right = (2 * i) + 2)
    - Iterate all nodes in level and reset index
    - At each level iteration, find maximum width (last - first + 1)

```java

class Pair {
    TreeNode node;
    int index;

    public Pair(TreeNode _node, int _index) {
        index = _index;
        node = _node;
    }
}
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        
        int ans = 0;
        // edge case
        if (root == null) return ans;

        Queue<Pair> queue = new LinkedList<>();

        // add root to the queue
        queue.offer(new Pair(root, 0));

        while (!queue.isEmpty()) {
            // index of the left most node which has minimum index at each level
            int minIndex = queue.peek().index;
            int size = queue.size();
            int firstInd = 0;
            int lastInd = 0;

            // iterate all nodes at the level
            for (int i = 0;  i < size; i++) {
                // index resetting to prevent overflow error for huge tree ~ 10^5
                int nextLevelIndex = queue.peek().index - minIndex;
                TreeNode node = queue.peek().node;

                queue.poll();

                // index of the first node in that level
                if (i == 0) firstInd = nextLevelIndex;

                // index of the last node in that level
                if (i == size - 1) lastInd = nextLevelIndex;
                
                if (node.left != null) {
                    queue.offer(new Pair(node.left, (nextLevelIndex * 2) + 1));
                }
                if (node.right != null) {
                    queue.offer(new Pair(node.right, (nextLevelIndex * 2) + 2));
                }
            }

            // calculate max width at each level
            ans = Math.max(ans, lastInd - firstInd + 1);
        }

        return ans;
    }
}

```