**Time Complexity:** O(n), where n is the number of people, as we are simply iterating through the list once.
**Space Complexity:** O(1), since we are not using any additional data structures.

```java

class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {

        int time = 0;

        for (int i = 0; i < tickets.length; i++) {
            if (i <= k) {
                // if i is before k, i will be able to buy min of either i or k before k is done buying all tickets
                time += Math.min(tickets[i], tickets[k]);
            } else {
                // If ithe come after k, then i will be able to buy max kth times - 1 as once k is done buying, ith turn won't come
                time += Math.min(tickets[i], tickets[k] - 1);
            }
        }
        
        return time;
    }
}

```