- **Time Complexity:** O(N), O(N) => parent marking + O(N) => traversal from traget to k level
- **Space Complexity:** O(N), for queue and hashmap
- **Approach:** SV - LO traversal by marking each node with its parent
    - First mark all nodes with its parent using level order traversal and hash map (node, parent)
    - Start iterating from target node and maintain which nodes are already visited using map
    - Traverse next level left, right and parent from node, if node is already traversed then skip it
    - If current level is k that mean we reached to max allowable level. Stop tree iteration and all nodes available in queue are nodes at distance k

```java

class Solution {

    // first mark all nodes with its parent using level order traversal and hash map (node, parent)
    private void markParent(TreeNode root, Map<TreeNode, TreeNode> map) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()) {
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    map.put(node.left, node);
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    map.put(node.right, node);
                    queue.offer(node.right);
                }
            } 
        }
    }
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        List<Integer> result = new ArrayList<>();

        if (root == null) {
            return result;
        }

        Map<TreeNode, TreeNode> trackParent = new HashMap<>();
        // first mark all nodes with its parent using level order traversal and hash map (node, parent)
        markParent(root, trackParent);

        Queue<TreeNode> queue = new LinkedList<>();
        // maintain which nodes are already visited using map
        Map<TreeNode, Boolean> visited = new HashMap<>();
        int curr_level = 0;

        // start iterating from target node
        queue.offer(target);
        visited.put(target, true);

        // iterate nodes in next level from target using LO traversal
        while (!queue.isEmpty()) {
            int size = queue.size();
        
            // if current level is k that mean we reached to max allowable level. Stop tree iteration and all nodes available in queue are nodes at distance k
            if (curr_level == k) break;

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();

                // traverse next level left, right and parent from node
                // if node is already traversed then skip it
                if (node.left != null && !visited.containsKey(node.left)) {
                    queue.offer(node.left);
                    visited.put(node.left, true);

                }
                if (node.right != null && !visited.containsKey(node.right)) {
                    queue.offer(node.right);
                    visited.put(node.right, true);

                }
                if (trackParent.get(node) != null && !visited.containsKey(trackParent.get(node))) {
                    TreeNode parent = trackParent.get(node);
                    queue.offer(parent);
                    visited.put(parent, true);
                }
            }
            curr_level++;
        }

        // iterate all remaining nodes from queue which are at distance k
        while(!queue.isEmpty()) {
            result.add(queue.poll().val);
        }

        return result;
    }
}

```