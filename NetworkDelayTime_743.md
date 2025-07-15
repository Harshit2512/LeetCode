
```java
public class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        Map<Integer, List<int[]>> graph = new HashMap<>();
        for (int[] time : times) {
            graph.computeIfAbsent(time[0], k -> new ArrayList<>()).add(new int[]{time[1], time[2]});
        }

        // Priority queue: (time, node)
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
        pq.add(new int[]{0, K});
        
        // Distance table
        Map<Integer, Integer> dist = new HashMap<>();
        dist.put(K, 0);
        
        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int currentTime = current[0];
            int currentNode = current[1];
            
            if (!graph.containsKey(currentNode)) {
                continue;
            }
            
            // Process neighbors
            for (int[] neighbor : graph.get(currentNode)) {
                int nextNode = neighbor[0];
                int timeToNext = neighbor[1];
                int newTime = currentTime + timeToNext;
                
                if (newTime < dist.getOrDefault(nextNode, Integer.MAX_VALUE)) {
                    dist.put(nextNode, newTime);
                    pq.add(new int[]{newTime, nextNode});
                }
            }
        }
        
        int maxDelay = 0;
        for (int delay : dist.values()) {
            maxDelay = Math.max(maxDelay, delay);
        }
        
        return dist.size() == N ? maxDelay : -1; // If not all nodes are reachable, return -1
    }
}
```