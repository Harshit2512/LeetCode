- **Time Complexity:** 
    -  Preprocessing: O(N log N) due to insertions into the tree map.
    -  Pick Index: O(log N) since searching through the TreeMap is logarithmic on average.
- **Space Complexity:** O(N) due to storing the cumulative sums in the TreeMap.
- **Key Points:**
    - Use TreeMap which supports dynamic binary search operation
    - Find total running sum, which is used to generate random number from range (0, totalSum)
    - Use tree map function map.higherEntry(target).getValue() to find smallest key greater than target

```java
class Solution {

    private TreeMap<Integer, Integer> map;
    private int totalSum;
    private Random rand;

    public Solution(int[] w) {
        this.map = new TreeMap<>();
        this.rand = new Random();
        this.totalSum = 0;
        int runningSum = 0;

        for (int i = 0; i < w.length; i++) {
            runningSum += w[i];
            map.put(runningSum, i);
        }
        this.totalSum = runningSum;     
    }
    
    public int pickIndex() {

        int target = rand.nextInt(totalSum);
        // Find the smallest key greater than target. This gives the cumulative weight.
        return map.higherEntry(target).getValue();
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
 ```