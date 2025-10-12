- **Time Complexity:** O(n),  We make a single pass over the intervals
- **Space Complexity:** O(n), We store the result in a new list which, in the worst case, could be as large as the input.
- **Key Points:**
    - Add all non overlapping intervals that comes before new interval
    - Merge overlapping intervals and add it to result
    - Add all non overlapping intervals that comes after new interval i.e. remaining intervals

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        
        List<int[]> result = new ArrayList<>();

        int i = 0;
        int n = intervals.length;

        // Add all non overlapping intervals that comes before new interval
        while (i < n && intervals[i][1] < newInterval[0]) {
            result.add(intervals[i]);
            i++;
        }

        // Merge overlapping intervals
        while (i < n && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = Math.min(intervals[i][0], newInterval[0]);
            newInterval[1] = Math.max(intervals[i][1], newInterval[1]);
            i++;
        }

        // Add merged overlapping interval
        result.add(newInterval);

        // Add all non overlapping intervals that comes after new interval i.e. remaining intervals
        while (i < n) {
            result.add(intervals[i]);
            i++;
        }

        return result.toArray(new int[result.size()][]);
    }
}
```