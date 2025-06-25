- **Time Complexity:**
    - Adding a number: O(log n) due to the insertion operation in heaps.
    - Finding median: O(1).
- **Space Complexity:** O(n) to store the numbers in the heaps.
- **Key Points:**
    - Use max and min heap to store lower half and upper half of numbers respectively
    - If num is less or equal largest value in max heap then add in max heap otherwise add in min heap
    - Balance heaps to max heap have 1 greater or equal value than min heap
    - If max heap has more value then there are odd numbers and return largest value of max heap
    - Else are are event numbers and median is largest from max heap plus smallest of minheap / 2

```java
class MedianFinder {

    // Max heap to store lower half values
    PriorityQueue<Integer> maxHeap;
    // Min heap to store upper half values
    PriorityQueue<Integer> minHeap;

    public MedianFinder() {
        maxHeap = new PriorityQueue<>((a, b) -> b - a);
        minHeap = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        // Add values to heaps
        if (maxHeap.isEmpty() || num <= maxHeap.peek()) {
            maxHeap.add(num);
        } else {
            minHeap.add(num);
        }

        // Balance heaps to max heap have 1 greater or equal value than min heap
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.add(maxHeap.poll());
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.add(minHeap.poll());
        }
    }
    
    public double findMedian() {
        // If max heap has more value then there are odd numbers and return largest value of max heap
        if (maxHeap.size() > minHeap.size()) {
            return maxHeap.peek();
        } else {
            // else are are event numbers and median is largest from max heap plus smallest of minheap / 2
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
        
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
 ```