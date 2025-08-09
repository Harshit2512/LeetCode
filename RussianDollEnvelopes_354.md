- **Time Complexity:** O(n log n) for sorting and binary search operations.
- **Space Complexity:** O(n) for storing the LIS.
- **Key Points:**
    - Sort input array - sort by width in ASC order, if width is same then sort by height in DESC order
    - Create a dynamic list dp to store the current best sequence of increasing envelope heights (we will apply LIS here).
    - find the index where height stored in DP list using binary search. Based on index, decide where should height be inserted/updated in DP list
    - If index is equal size of DP list that means this height is highest among all heights found till now and insert at the end. Otherwise update height at existing index

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        
        if (envelopes.length == 0) return 0;

        // Sort input array - sort by width in ASC order, if width is same then sort by height in DESC order
        // we sort by descending height to prevent these from contributing to the LIS

        Arrays.sort(envelopes, (a, b) -> {
            if (a[0] == b[0]) return b[1] - a[1];
            return a[0] - b[0];
        });

        // Create a dynamic list dp to store the current best sequence of increasing envelope heights (we will apply LIS here).
        List<Integer> dp = new ArrayList<>();

        for (int[] env : envelopes) {
            int height = env[1];

            // find the index where height stored in DP list using binary search
            int index = Collections.binarySearch(dp, height);

            // Based on index, decide where should height be inserted/updated in DP list
            if (index < 0) {
                index = -(index + 1);
            } 
            // If index is equal size of DP list that means this height is highest among all heights found till now and insert at the end
            if (index == dp.size()) {
                dp.add(height);
            }
            // otherwise update height at existing index
            else {
                dp.set(index, height);
            }
        } 
        return dp.size();
    }
}
```