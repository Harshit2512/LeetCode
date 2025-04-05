- **Time Complexity:** O(1) on average for each call to next, because each element is pushed and popped from the stack at most once.
- **Space Complexity:** O(n) for storing elements in the stack where n is the number of prices recorded.
- **KP:**
    - See how logic using stack is formed to cover all previous elements to compare with current

```java
class StockSpanner {

    Stack<int[]> stockSpan; // each stack element is array of [price, span]

    public StockSpanner() {
        stockSpan = new Stack<>();
    }
    
    public int next(int price) {
        int span = 1; // current input's span itself = 1
        
        // compare current price with each stack element until stack elements price is less than current price
        while (!stockSpan.isEmpty() && stockSpan.peek()[0] <= price) {
            span += stockSpan.pop()[1]; // is stack element price is less, increase span
        }
        
        // push each current price with latest updated span in stack
        stockSpan.push(new int[]{price, span});
        return span;
    }
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner obj = new StockSpanner();
 * int param_1 = obj.next(price);
 */

```