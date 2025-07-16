- **Time Complexity:** O(E log V) where E is the number of flights. The log factor comes from the priority queue.
- **Space Complexity:** O(V * E) due to adjacency list and priority queue.
- **Key Points:**
    - Use Djikstra algorithm to find minimum cost
    - Use a priority queue to always select the current minimum cost path.
    - Keep track of costs and number of stops made.
    - If we reach a destination before exceeding K stops, we found the solution.
    - Use an array to store the minimum cost to reach each city within a certain number of stops.

```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {

        // Min heap to store dest with min cost -> {cost, dest, stops}
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
        Map<Integer, List<int[]>> graph = new HashMap<>(); // adjacency list

        // create adjacency list
        for (int[] flight : flights) {
            graph.computeIfAbsent(flight[0], z -> new ArrayList<>()).add(new int[]{flight[1], flight[2]});
        }

        int[] minCost = new int[n];
        Arrays.fill(minCost, Integer.MAX_VALUE);
        // put src in the PQ to begin with
        pq.offer(new int[]{0, src, 0});

        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int cost = current[0];
            int city = current[1];
            int stop = current[2];

            // dest is reached with allowed stops and return cost as min cost
            if (city == dst) return cost;

            if (stop <= k) {
                // traverse all neighbor cities of current city from adj list
                for (int[] next : graph.getOrDefault(city, new ArrayList<>())) {
                    int newCost = cost + next[1];
                    if (newCost < minCost[next[0]]) {
                        minCost[next[0]] = newCost;
                        pq.offer(new int[]{newCost, next[0], stop + 1});
                    }
                }
            } 
        }

        return -1;
    }
}
```