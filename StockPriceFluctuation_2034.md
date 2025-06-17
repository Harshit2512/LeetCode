- Time Complexity: 
    - update: O(log n) for both adding the new timestamp-price pair and updating counting in the count map.
    - current: O(1) using TreeMap's floor function.
    - maximum and minimum: O(1) to directly access the max and min keys in the count TreeMap.
- Space Complexity: O(n) as we store prices and counts for up to n different timestamps.
- Key Points:
    - Use TreeMap which stores keys in sorted array and helps in find min and max in constant time
    - Maintain price map for prices and count map for price ocurances which gives min and max using TreeMap's function

```java
class StockPrice {
    
    TreeMap<Integer, Integer> prices;
    TreeMap<Integer, Integer> count;
    int maxTimeStamp;

    public StockPrice() {
        prices = new TreeMap<>();
        count = new TreeMap<>();
        maxTimeStamp = 0;    
    }
    
    public void update(int timestamp, int price) {

        // If key already exist then get old price and check occurance of old price. If occurance is 0 then remove from count map
        if (prices.containsKey(timestamp)) {
            int oldPrice = prices.get(timestamp);
            count.put(oldPrice, count.get(oldPrice) - 1);
            if (count.get(oldPrice) == 0) {
                count.remove(oldPrice);
            }
        }

        // Update prices and count maps
        prices.put(timestamp, price);
        count.put(price, count.getOrDefault(price, 0) + 1);
        maxTimeStamp = Math.max(maxTimeStamp, timestamp);
    }
    
    public int current() {
        return prices.get(maxTimeStamp);
    }
    
    public int maximum() {
        return count.lastKey();
    }
    
    public int minimum() {
        return count.firstKey();
    }
}

/**
 * Your StockPrice object will be instantiated and called as such:
 * StockPrice obj = new StockPrice();
 * obj.update(timestamp,price);
 * int param_2 = obj.current();
 * int param_3 = obj.maximum();
 * int param_4 = obj.minimum();
 */
 ```