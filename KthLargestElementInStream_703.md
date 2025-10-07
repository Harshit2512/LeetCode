- **Time Complexity:** O(Nlogk) For Initialization, O(logk) For Add. Overall O(logk) : for each addition (heap insertion and adjustment)
- **Space Complexity:** O(k) for maintaining the heap of size k
- **Key Points:**
    - Approach: optimal approach using minheap since here stream is unsorted. if it were sorted, we could have used binary search to define index
    - Use a PriorityQueue (min-heap) of size k.
    - Iterate over the initial list and add each element to the heap.
    - If the heap exceeds size k, remove the smallest element (top of the heap).
    - For a new addition, add the element and ensure the heap does not exceed size k.
    - The top element of the heap will be the k-th largest element

```java
class KthLargest {

    // member variable initialization
    private final int k;
    private final PriorityQueue<Integer> minHeap;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        this.minHeap = new PriorityQueue();

        // Iterate and add val into minheap
        for (int num : nums) {
            add(num);
        }
    }
    
    public int add(int val) {
        // add value into heap
        minHeap.offer(val);

        // minHeap condition : need to track only first k elements, so if size exceeds k then remove min element
        if (minHeap.size() > k) {
            minHeap.poll();
        }

        // element at root will give kth largest element
        return minHeap.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
 ```