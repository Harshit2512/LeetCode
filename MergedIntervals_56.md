- **Time Complexity:** O(n log n), where n is the number of intervals. Sorting the intervals dominates the time complexity.
- **Space Complexity:** O(n), used for storing the merged intervals.
- **Key Points:**
    - Sort the list of intervals based on the starting time.
    - Iterate through sorted intervals.
    - Compare the current interval with the last merged interval: If they overlap, merge them. If not, simply add the current interval to the result.

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        
        // Base case: if only one interval then return as is
        if (intervals.length <= 1) {
            return intervals;
        }

        // sort intervals in ascending order by starting number (ascending -> a[0] - b[0])
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        LinkedList<int[]> merged = new LinkedList<>();

        // Iterate intervals to produce merged intervals
        for (int[] interval : intervals) {

            // add in list if merged list is empty or end of last element is less than start of current interval (no overlapping)
            if (merged.isEmpty() || merged.getLast()[1] < interval[0]) {
                merged.add(interval);
            } else {
                // there is overlapping intervals, adjust end for overlapping interval 
                merged.getLast()[1] = Math.max(merged.getLast()[1], interval[1]);
            }
        }

        // return result in 2D array
        return merged.toArray(new int[merged.size()][]);
    }
}
```