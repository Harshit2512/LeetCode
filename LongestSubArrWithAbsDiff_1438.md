- **Time Complexity:** O(N), Each element is added and removed from the deque at most once.
- **Space Complexity:** O(N), Space for the two deques holding indices.
- **Key Points:**
    - Dequeue logic optimizes the need of finding min and max from sub arrays
    - MaxQueue : maintains max number. Monotonically decreasing queue, if current number is larger than first num in Q, then remove pre and add current
    - MinQueue : Maintains min number. Monotonically increasing queue, if current number is smaller than first num in Q, then remove pre and add current

```java

class Solution {
    public int longestSubarray(int[] nums, int limit) {
        
        Deque<Integer> maxQueue = new LinkedList<>();
        Deque<Integer> minQueue = new LinkedList<>();
        int left = 0, right;
        int maxLen = 0;

        for (right = 0; right < nums.length; right++) {
            // if current is lesser than last in Min Q, then remove Q last
            while (!minQueue.isEmpty() && nums[minQueue.peekLast()] > nums[right]) {
                minQueue.pollLast();
            }
            minQueue.offerLast(right);
            
            // if current is more greater than last in Max Q, then remove Q last
            while (!maxQueue.isEmpty() && nums[maxQueue.peekLast()] < nums[right]) {
                maxQueue.pollLast();
            }
            maxQueue.offerLast(right);

            // Find the diff of min and max and if less than limit, slide the window by moving left pointer
            while (nums[maxQueue.peekFirst()] - nums[minQueue.peekFirst()] > limit) {
                left++;

                // if left pointer is moved then we also need to remove pre element from queues
                if (maxQueue.peekFirst() < left) {
                    maxQueue.pollFirst();
                }
                if (minQueue.peekFirst() < left) {
                    minQueue.pollFirst();
                }
            }

            maxLen = Math.max(maxLen, right - left + 1);
        }

        return maxLen;
    }
}

```