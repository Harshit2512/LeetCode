- **Time Complexity:** O(N log N ), if PQ is used or O(N)
- **Space Complexity:** O(N)
- When to use PQ - If it's asked that get  the node on same level by value in ASC order instead of from left to right
- Premium question

- **Solution 1 - Using x-y system**

```java

class Tuple {
    TreeNode node;
    int row;
    int col;

    public Tuple(TreeNode _node, int _row, int _col) {
        node = _node;
        row = _row;
        col = _col;
    }
}

class Solution {
    public List<List<Integer>> verticalOrder(TreeNode root) {
        
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        TreeMap<Integer, TreeMap<Integer, LinkedList<Integer>>> map = new TreeMap<>();
        Queue<Tuple> queue = new LinkedList<Tuple>();

        // Base case - null BT
        if (root == null) {
            return result;
        }

        // Put root into the queue
        queue.offer(new Tuple(root, 0, 0));

        while (!queue.isEmpty()) {
            Tuple tuple = queue.poll();
            TreeNode node = tuple.node;
            int row = tuple.row;
            int col = tuple.col;

            // Check if Horizontal level key is already present in map, if not present then create key & value
            if (!map.containsKey(row)) {
                map.put(row, new TreeMap<>());
            }

            // Check if for horizontal level, vertical level key present or not
            if (!map.get(row).containsKey(col)) {
                map.get(row).put(col, new LinkedList<>());
            }

            // Add current node value in PQ for given vertical key
            map.get(row).get(col).offer(node.val);

            // Iterate left and right child and put in queue
            // For left child, decrease x axis value (col) and increase H level
            if (node.left != null) queue.offer(new Tuple(node.left, row - 1, col + 1));

            // For right child, increase x axis value (col) and increase H level
            if (node.right != null) queue.offer(new Tuple(node.right, row + 1, col + 1));

        }

        // Read map value for V level and nodes on that level
        for (TreeMap<Integer, LinkedList<Integer>> yNodes : map.values()) {
            // Store each V level nodes as List in main List
            result.add(new ArrayList<>());

            // Iterate each V level nodes from PQ
            for (LinkedList<Integer> nodes : yNodes.values()) {
                while (!nodes.isEmpty()) {
                    result.get(result.size() - 1).add(nodes.poll());;
                }
            }
        }

        return result;

    }
}

```

- **Solution 2 - Without x-y system**

```java

class Solution {
    public List<List<Integer>> verticalOrder(TreeNode root) {
        if(root == null) return new ArrayList();
        
        List<List<Integer>> result = new ArrayList<>();
        Map<Integer, List> columnList = new HashMap<>();
        Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();
        int minColumn = 0, maxColumn = 0;
        queue.add(new Pair(root, 0));

        while(!queue.isEmpty()) {
            int size = queue.size();
            for(int i=0; i<size; i++) {
                Pair<TreeNode, Integer> p = queue.poll();
                TreeNode cur = p.getKey();
                int column = p.getValue();

                if(!columnList.containsKey(column)) {
                    columnList.put(column, new ArrayList());
                }
                columnList.get(column).add(cur.val);
                minColumn = Math.min(minColumn, column);
                maxColumn = Math.max(maxColumn, column);

                if(cur.left != null) {
                    queue.add(new Pair(cur.left, column - 1));
                }
                if(cur.right != null) {
                    queue.add(new Pair(cur.right, column + 1));
                }
            }
        }
 
        for(int i=minColumn; i<=maxColumn; i++) {
            result.add(columnList.get(i));
        }
        return result;
    }
}

```

![Alternative Text](https://github.com/Harshit2512/LeetCode/blob/main/images/314_image1.jpg)
![Alternative Text](https://github.com/Harshit2512/LeetCode/blob/main/images/314_image2.jpg)