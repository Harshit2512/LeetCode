- **Key Points:**
    - See how max ele are maintained in case of both solution
    - Priority Queue: Don't remove elements within window to get the max element. PQ will sort the elements and keep the largest el at the head of the PQ
    - Deque: Need to remove all non-greater elements withing window to keep only greater el at the head of the Q.

```java

class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // Time Complexity: O(N): Each element is added and removed from the deque at most once.
        // Space Complexity: O(K): Deque holds at most K elements.
        // This approach has lower runtime 33 ms, where as approach with PriorityQueue has runtime 87 ms though time complexity of O(N Log K)

        // edge case
        if (nums == null || nums.length == 0) return new int[0];
        
        Deque<Integer> maxQueue = new ArrayDeque<>();
        int[] max = new int[nums.length - k + 1];

        for (int i = 0; i < nums.length; i++) {
            // if for current el, Q is about to go out of window then remove elements from the head
            while (!maxQueue.isEmpty() && maxQueue.peekFirst() < i - k + 1) {
                maxQueue.pollFirst();
            }

            // Keep only greater elements than current el in the queue, remove all non greater elements
            while (!maxQueue.isEmpty() && nums[maxQueue.peekLast()] < nums[i]) {
                maxQueue.pollLast();
            }
            
            // Put current el in the Q at last
            maxQueue.offerLast(i);

            // If window is filled then find the max num in the window by peeking the head of the Q
            if (i - k + 1 >= 0) {
                max[i - k + 1] = nums[maxQueue.peekFirst()];
            }
        }
        return max;

        // Time Complexity: O(N log K): For each of the N elements, we insert and/or delete from the heap which has a log K time complexity.
        // Space Complexity: O(K): Max heap can hold up to K elements.

        // This approach has higher runtime 87 ms, where as approach with Dequeue is more optimum with runtime 12 ms
        // if (nums == null || nums.length == 0) return new int[0];

        // PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
        // int[] max = new int[nums.length - k + 1];

        // for (int i = 0; i < nums.length; i++) {
        //     // if for current el, Q is about to go out of window then remove elements
        //     while (!maxHeap.isEmpty() && maxHeap.peek()[1] < i - k + 1) {
        //         maxHeap.poll();
        //     }
            
        //     // Put current el in the Q
        //     maxHeap.offer(new int[]{nums[i], i});

        //     // If window is filled then find the max num in the window by peeking the head of the Q
        //     if (i - k + 1 >= 0) {
        //         max[i - k + 1] = maxHeap.peek()[0];
        //     }
        // }
        // return max;
        
    }
}

```