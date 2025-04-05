- **Time Complexity:** O(n), where n is the number of people in the queue. Each person is pushed and popped from the stack at most once.
- **Space Complexity:** O(n), for the stack that keeps track of indices.
- **Key Points:**
    - maintain a stack to keep only taller people bcz they may be seen by other people in the future ele iteration 

```java
class Solution {
    public int[] canSeePersonsCount(int[] heights) {

        int[] result = new int[heights.length];
        Stack<Integer> stack = new Stack<>();

        // start from right end since for each ele w need to consider all available ele right side
        for (int i = heights.length - 1; i >= 0; i--) {
            int visible = 0; // initial visible count for current person
            

            // only keep taller person in stack bcz they may be seen other person as well
            //heights[i] > stack.peek()
            while (!stack.isEmpty() && heights[i] > heights[stack.peek()]) {
                visible++;
                stack.pop();
            }

            // handle the case where current ele (person) is shorter than right next person (which was not seen 
            // from stack in while condition) but is visible due to immediate right next
            if (!stack.isEmpty()) {
                visible++;
            }

            stack.push(i);
            //stack.push(heights[i]); we can also push height directly to the stack instead of index
            result[i] = visible;
        }

        return result;
        
    }
}
```