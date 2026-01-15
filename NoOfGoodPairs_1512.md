- **Time Complexity:** O(N)
- **Space Complexity:** O(N), store N elements in Map
- **Approach:** Using HashMap
    - If num is not present in Map then store it with freq 1
    - If num is present in map, it means it has appeared before. And no of times it appreared before, that many times current num can make a pair with.
    - Keep adding all pair count to counter variable. Final value of counter var will be answer

``` java
// Optimized approach with Map

public class Solution {
    public int numIdenticalPairs(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int count = 0;
        
        // Iterate over each number in the array
        for (int num : nums) {
            // If number is already seen, it can form pairs with all previous occurrences
            if (map.containsKey(num)) {
                // Increment count by the number of occurrences seen so far
                count += map.get(num);
                // Increment the occurrence count in the map
                map.put(num, map.get(num) + 1);
            } else {
                // If number is seen for the first time, put it in the map
                map.put(num, 1);
            }
        }
        return count;
    }
}

// Brute force approach using two for loops

public class Solution {
    public int numIdenticalPairs(int[] nums) {
        int count = 0;
        // Outer loop to fix the first element of the pair
        for (int i = 0; i < nums.length; i++) {
            // Inner loop to fix the second element of the pair
            for (int j = i + 1; j < nums.length; j++) {
                // Check if we have a good pair
                if (nums[i] == nums[j]) {
                    count++;
                }
            }
        }
        return count;
    }
}

```

