- **Time Complexity** - (NlogN) N - no of intervals and logN - sorting TC for minHeap
- **Space Complexity** - O(N), worst case if all meetings require separate meeting room in case of overlap
- **Approach:** minHeap to maintain occupied meeting rooms and room with shortest end time on top
    - Sort the meeting by start time
    - Iterate intervals and check there is no overlap for current meeting with meeting (minHeap top) that has shortest end time
    - If no overlap, use existing room and increase meeting room's occupied time OR there is an overlap and need a new room (add  to minHeap)
    - Add updated previous back into the heap with increased end time (no overlap and new meeting) OR without increased end time (overlap)

```java

class Solution {
    public int minMeetingRooms(int[][] intervals) {
        // sorting the meeting by start time
        Arrays.sort(intervals, (a,b) -> a[0]-b[0]);

        // minHeap to store meetings that has shortest end time at top
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a,b) -> a[1]-b[1]);

        minHeap.add(intervals[0]);

        for(int i = 1; i < intervals.length; i++) {
            int[] current = intervals[i];
            int[] previous = minHeap.remove();

            // check if there is no overlap
            if(current[0] >= previous[1]) {//use existing room
                // increase meeting room's occupied time
                previous[1] = current[1];
            } else { // there is an overlap need a new room
                minHeap.add(current);
            }
            //add updated previous back into the heap
            minHeap.add(previous);
        }
        return minHeap.size();
    }
}

```