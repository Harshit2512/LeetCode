- **Time Complexity:** O(N), since each employee is visited once.
- **Space Complexity:** O(N), which is the recursion stack depth in the worst case.
- **Key Points:**
    - Create subordinates list for each employee and fill subordinates list
    - Find time taken for each sbordinate recursively

```java
class Solution {
    int maxTime = 0;
    public int numOfMinutes(int n, int headID, int[] manager, int[] informTime) {
        List<List<Integer>> subordinates = new ArrayList<>();
        

        // Create subordinates list for each employee
        for (int i = 0; i < n; i++) {
            subordinates.add(new ArrayList<>());
        }

        // Fill subordinates list
        for (int j = 0; j < n; j++) {
            if (manager[j] != -1) {
                subordinates.get(manager[j]).add(j);
            }         
        }

        dfs(headID, 0, subordinates, informTime);
        return maxTime;
    }

    private void dfs(int currentId, int currentTime, List<List<Integer>> subordinates, int[] informTime) {
        maxTime = Math.max(maxTime, currentTime); 

        // find time take for each sbordinate recursively
        for (int sub : subordinates.get(currentId)) {
            dfs(sub, currentTime + informTime[currentId], subordinates, informTime);
        }
    }
}
```