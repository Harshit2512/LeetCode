- **Time Complexity:** Each ping operation is O(1) on average since we are performing operations that affect only the current and the oldest timestamps.
- **Space Complexity:** O(n) where n is the number of timestamps in the last 3000 milliseconds. (push each ping ele to queue)

```java

class RecentCounter {

    Queue<Integer> calls;

    public RecentCounter() {
        calls = new LinkedList<>(); 
    }
    
    public int ping(int t) {
        
        // First put each call to queue
        calls.offer(t);

        // Remove all calls which are older that 3000 ms
        while (calls.peek() < t - 3000) {
            calls.poll();
        }

        // queue size returns the no of calls in last 3000 ms
        return calls.size();
    }
}

/**
 * Your RecentCounter object will be instantiated and called as such:
 * RecentCounter obj = new RecentCounter();
 * int param_1 = obj.ping(t);
 */

 ```