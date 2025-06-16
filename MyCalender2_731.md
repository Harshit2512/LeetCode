- **Time Complexity:** O(N), where N is N is the no of bookings we need to check in bookings and overlapping bookings
- **Space Complexity:** O(N), max we might need to add N bookings
- **Key Points:**
    - Track bookings and overlapping bookings in two separate lists
    - If current interval exist in overlapping list zthen triple booking and not allowed
    - If not then check if overlap can be made with any of from existing booking. If yes then add common interval as overlap in overlapping list
    - Also add current interval in mapping list 

```java
class MyCalendarTwo {

    List<int[]> overlapping;
    List<int[]> bookings;

    public MyCalendarTwo() {
        overlapping = new ArrayList<>();
        bookings = new ArrayList<>();    
    }
    
    public boolean book(int startTime, int endTime) {
        
        // First check if given start and end tim einterval is already available in overlapping list, if yes then it's triple booking

        for (int[] overlap : overlapping) {
            if (startTime < overlap[1] && endTime > overlap[0]) {
                return false;
            }
        }

        // if no overlap found then booking can be made, Add interval in overlapping list if any overlap can be found from existing bookings
        for (int[] booking : bookings) {
            if (startTime < booking[1] && endTime > booking[0]) {
                overlapping.add(new int[]{Math.max(startTime, booking[0]), Math.min(endTime, booking[1])});
            }
        }

        // After add new interval in booking list
        bookings.add(new int[]{startTime, endTime});
        return true;

    }
}

/**
 * Your MyCalendarTwo object will be instantiated and called as such:
 * MyCalendarTwo obj = new MyCalendarTwo();
 * boolean param_1 = obj.book(startTime,endTime);
 **/
 ```***