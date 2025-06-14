- **Time Complexity:** O(log n) due to the TreeMap operations (floor, ceiling, and put).
- **Space Complexity:** O(n) for storing the intervals in the TreeMap.
- **Key Points:**
    - Use TreeMap to store cal entries in sorted order which reduce the lookup time for overlap checks using its natural ordering properties
    - find prev and next entries from cal using floorKey and ceilingKey and compare current start and end time to check overlap

```java
class MyCalendar {

    TreeMap<Integer, Integer> calMap;
    public MyCalendar() {
        calMap = new TreeMap<>(); 
    }
    
    public boolean book(int startTime, int endTime) {
        
        // possible prev entry in cal: Find the start time (largest key) from calMap which is less than or equal to the current startTime
        Integer prev = calMap.floorKey(startTime);

        // possible next entry in cal: Find the start time (smallest key) from calMap which is greater than or equal to the current startTime
        Integer next = calMap.ceilingKey(startTime);

        // If start and end time overlaps then return false
        if ((prev != null && calMap.get(prev) > startTime) || (next != null && endTime > next)) {
            return false;
        }

        calMap.put(startTime, endTime);
        return true;
    }
}

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar obj = new MyCalendar();
 * boolean param_1 = obj.book(startTime,endTime);
 */
 ```