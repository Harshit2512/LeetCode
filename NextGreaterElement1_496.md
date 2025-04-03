- **Time Complexity:** O(n + m), iterating nums2 once O(m), and checking each nums1 element (n) in O(1) using the hashmap.
- **Space Complexity:** O(m), (nums2 = m) for storing the hashmap and the stack.
- **Key Points:**
    - Use monotonic stack to find next greater for each elements

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
       
        Map<Integer, Integer> map = new HashMap<>();
        Stack<Integer> stack = new Stack<>();

        // For each element in nums2, find next greater element and store in map
        // storing nums2 on stack reduce time complexity by nested for loops to 
        // find next greater for each element
        for (int num : nums2) {
            while (!stack.isEmpty() && stack.peek() < num) {
                map.put(stack.pop(), num);
            }

            // push element to the stack
            stack.push(num);
            
        }

        int[] result = new int[nums1.length];

        // get next greater element for each element of nums1
        for (int i = 0; i < nums1.length; i++) {
            result[i] = map.getOrDefault(nums1[i], -1);
        }

        return result;
    }
}
```