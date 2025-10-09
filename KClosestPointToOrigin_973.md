- **Time Complexity:** O(N log K), where N is the number of points and K is the number of closest points required. This is due to the priority queue operations.
- **Space Complexity:** O(K), for storing the K closest points in the heap.
- **Key Points:**
    - PQ/Max Heap approach to store k elements in sorted way
    - Create a max heap (priority queue) that will store the points based on their distance from the origin.
    - Iterate through each point and calculate its distance from the origin.
    - Maintain the heap to only contain the K closest points by removing the farthest point when the heap size exceeds K.
    - Convert the result from the heap to an array and return it.

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        
        // Intialize maxHeap to store in desc order, being max at the root
        // 0 index corresponds to x coordinate and 1 index corresponds to y coordinate
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> (b[0] * b[0] + b[1] * b[1]) - (a[0] * a[0] + a[1] * a[1]));

        // Insert points in maxHeap with size k
        for (int[] point : points) {
            maxHeap.offer(point);
            // If size exceeds k then remove max from PQ
            if (maxHeap.size() > k) {
                maxHeap.poll();
            }
        }

        // Initialize result array of size k
        int[][] result = new int[k][2];

        for (int i = 0; i < k; i++) {
            result[i] = maxHeap.poll();
        }

        return result;
    }
}
```