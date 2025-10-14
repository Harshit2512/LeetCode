- **Time Complexity:** O(N log N), N for iteration of intervals and N LogN for sorting array => N + N LogN = N (1 + LogN) = N LogN
- **Space Complexity:** O(1), no additional space required
- **Key Points:**
    - Sort the intervals by the end time to efficiently find the optimal position to 'cut' the intervals.
    - Initialize a counter for removals and set a variable for the end of the last added interval.
    - Traverse the sorted intervals and check if the current interval overlaps with the last non-overlapping interval.
    - If overlapped, increment the removal counter; otherwise, update the end point to the current interval’s end time.

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        // edge case: if input length is zero then return result as 0
        if (intervals.length == 0) return 0;

        // Sort array in ascending order by end element. Why not start -> sorting by start will give incorrect overlapping intervals and logic needs to be modified
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1]));

        int count = 0;
        int end = intervals[0][1]; // initial interval
        
        // Interate intervals and compare end of initial and current interval
        // If comes across overlapping interval then increase count and DONT update initial as we need it for other intervals check
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] < end ) {
                count++;
            } else {
                // If non-overlapping interval then update initial end to current interval
                end = intervals[i][1];
            }          
        }

        return count;
    }
}
```