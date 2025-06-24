- **Time Complexity:**
    - Sorting the tasks costs O(N log N), where N is the number of tasks.
    - The iteration over tasks is O(N).
- **Space Complexity:** O(N) is used to store the tasks and the processing order.
- **Key points:**
    - Create new task array with task index and Sort the array to based on enqueue time (primary) and index(secondary)
    - Use Priority Queue (Min heap) to load all task in desc order of processing time (primary) and index of task (secondary)
    - If pq is not empty and enqueue time is less than or equal current time, then process the task
    - If pq is empty (CPU is ideal) then move forward current time to next task starting (enqueu) time

```java
class Solution {
    public int[] getOrder(int[][] tasks) {
        int taskLen = tasks.length;
        int[][] procTaskList = new int[taskLen][3];

        // add index of the task in the array as additional param to track the task 
        for (int i = 0; i < taskLen; i++) {
            procTaskList[i][0] = tasks[i][0];
            procTaskList[i][1] = tasks[i][1];
            procTaskList[i][2] = i;

        }

        // Sort the array based on enqueue time (primary) and index(secondary)
        Arrays.sort(procTaskList, (a, b) -> a[0] == b[0] ? Integer.compare(a[2], b[2]) : Integer.compare(a[0], b[0]));

        // process procTaskList using min heap
        int[] resultArr = new int[taskLen];
        int resultArrIndex = 0;
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] == b[1] ? Integer.compare(a[2], b[2]) : Integer.compare(a[1], b[1]));
        int i = 0;
        int currentTime = 0;

        while (i < procTaskList.length || !pq.isEmpty()) {

            // load all tasks to pq whose enqueue time (or index) is less than or equal to current time
            while (i < procTaskList.length && procTaskList[i][0] <= currentTime) {
                pq.offer(procTaskList[i++]);
            }

            if (!pq.isEmpty()) {
                // process the task based on shortest processing time
                int[] task = pq.poll();
                currentTime +=  task[1];
                resultArr[resultArrIndex++] = task[2];
            } else {
                // if CPU is idle, then move forward current time to next task starting time
                currentTime = procTaskList[i][0];
            }
        }

        return resultArr;
    }
}
```