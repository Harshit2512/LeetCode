- **Time Complexity:** The time complexity is O(n log k), where n is the number of buildings and k is the number of ladders, due to heap operations (insertion and deletion).
- **Space Complexity:** The space complexity is O(k), where k is the number of ladders, corresponding to the maximum size of the heap.
- **Key Points:**
    - Use min heap to optimize as ladder or bricks should be used
    - First use all ladders till available, after that use bricks and recover ladders if can
    - Once all ladders and bricks exhausted then return current index of the building


```java
class Solution {
    public int furthestBuilding(int[] heights, int bricks, int ladders) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(); // Min Heap, keep min diff at the front of heap

        for (int i = 0; i < heights.length - 1; i++) {
            int diff = heights[i+1] - heights[i];

            if (diff > 0) { // if diff > 0 then need to climb up using ladder or brick
                pq.add(diff);

                // First use available ladders, if ladders get exhausted use bricks
                // Until pq size is less than ladders, means using ladder
                // If used brick, poll diff from heap which means ladder got recovered in use of bricks
                if (pq.size() > ladders) { 
                    bricks = bricks - pq.poll();
                }

                // If after using bricks, if no more bricks left then can't go further so return index of current building
                if (bricks < 0) return i;
            }
            
        }

        // If reached all the way farther then return farthest building index
        return heights.length - 1;
    }
}
```