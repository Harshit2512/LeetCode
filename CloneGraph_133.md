- **Time Complexity:** O(N), where N is the number of nodes. Each node and edge is traversed once.
- **Space Complexity:** O(N) due to the recursion stack and hashmap storage of the nodes.
- **Key Points:**
    - Maintain a map for visited node and return node if already visited before
    - Perform DFS by visiting each node and cloning it. Then get neighbors of orinal node and add neighbors of in cloned node 

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    private Map<Node, Node> visited = new HashMap<>();
    
    public Node cloneGraph(Node node) {
        // Base case
        if (node == null) {
            return null;
        }

        // If the node was already visited, return the clone from the hashmap
        if (visited.containsKey(node)) {
            return visited.get(node);
        }

        // Create a clone for the node
        Node cloneNode = new Node(node.val);
        visited.put(node, cloneNode);

        // Iterate over the neighbors to populate the cloned graph
        for (Node neighbor : node.neighbors) {
            cloneNode.neighbors.add(cloneGraph(neighbor));
        }
        return cloneNode;
    }
}
```