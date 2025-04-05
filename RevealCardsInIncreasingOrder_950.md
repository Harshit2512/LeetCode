- **Time Complexity:** O(N log N) for sorting, and O(N) for queue operations, resulting in overall O(N log N).
- **Space Complexity:** O(N) for maintaining the queue.
- **Key Points:**
    - Use Array.sort to first arrange the deck in increasing as stated in problem
    - Use a queue to maintain the alternate card placing order in result

```java

class Solution {
    public int[] deckRevealedIncreasing(int[] deck) {
        int length = deck.length;
        int[] result = new int[length];
        Queue<Integer> queue = new LinkedList<>(); // queue to store indices to be able to follow the card placing order mentioned in question

        // sort the deck to be able to drawn in increasing order as required from question
        Arrays.sort(deck) ;


        // add all indices to the queue first
        for (int i = 0; i < length; i++) {
            queue.add(i);
        }

        // Draw the each card and place at alternate index
        for (int card : deck) {
            result[queue.poll()] = card;
            
            if (!queue.isEmpty()) {
                queue.add(queue.poll());
            }            
        }

        return result;
    }
}

```