- **Time Complexity:** The time complexity is O(E log V), where E is the number of edges and V is the number of vertices, due to the heap operations.
- **Space Complexity:** The space complexity is O(V + E), for storing the graph and the distance table.
- **Key Points:**
    - Djikstra algorith to find shortest path algorith
    - Create adjacency list from given input and define distance map (node, distanceToNode) with initial node K with initial value 0
    - PQ min heap (total distance, node) with initial K node with total node distance as 0
    - Poll PQ and traverse all neighbors of node. Calculate total distance to the neighbr node and update distance table if minimum distance found 

```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int K) {
        Map<Integer, List<int[]>> graph = new HashMap<>();

        // Create adjacency list - key -> value = source node -> { target node, time taken}
        for (int[] time : times) {
            graph.computeIfAbsent(time[0], k -> new ArrayList<>()).add(new int[]{time[1], time[2]});
            //graph.computeIfAbsent(time[0], k -> new ArrayList<>()).add(new int[]{time[1], time[2]});
        }
        
        // Define Priority Queue (Min heap) -> (time, node)
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
        pq.offer(new int[]{0, K});

        // Distance table
        Map<Integer, Integer> distance = new HashMap<>();
        distance.put(K, 0);

        while (!pq.isEmpty()) {
            int[] node = pq.poll();
            int currentTime = node[0];
            int currentNode = node[1];

            if (!graph.containsKey(currentNode)) continue; 

            // Process all neighbors
            for (int[] neighbor : graph.get(currentNode)) {
                int nextNode = neighbor[0];
                int timeToNextNode = neighbor[1];
                int newTime = currentTime + timeToNextNode;

                // Take only those neighors whose new time to reach is less than prev recorded time from distance map and add in pq
                if (newTime < distance.getOrDefault(nextNode, Integer.MAX_VALUE)) {
                    distance.put(nextNode, newTime);
                    pq.offer(new int[]{newTime, nextNode});
                }
            }
        }

        int maxDelay = 0;
        for (int delay : distance.values()) {
            maxDelay = Math.max(maxDelay, delay);
        }
        
        return distance.size() == n ? maxDelay : -1; // If not all nodes are reachable, return -1

    }
}
```