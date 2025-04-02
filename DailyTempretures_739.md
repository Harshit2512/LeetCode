// Time Complexity: O(n), each element is pushed and popped at most once.
// Space Complexity: O(n), due to the stack storing up to n indices.
// KP: 
// - Didn't actually store the temp value but stored index at which warmer temp evalution required
// - How stack was used to avoid two nested for loops to reduce time complexity

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int T = temperatures.length;
        Stack<Integer> stack = new Stack<>();
        int[] result = new int[T];

        for (int i = 0; i < T; i++) {

            // until stack is empty and current temp is greather than prev indices tempreture in the stack which are looking for warmer temp
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int index = stack.pop();
                result[index] = i - index;
            }

            stack.push(i); // push current temp to stack
        }

        return result;
        
    }
}