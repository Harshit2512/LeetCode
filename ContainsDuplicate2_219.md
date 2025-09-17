- **Time Complexity:** O(n): We iterate through the list once, each operation (add, remove, contains) of HashSet takes O(1) on average.
- **Space Complexity:** O(min(n, k)): The space used by the HashSet scales with the size of k, as it only keeps track of k elements at a time.
- **Key Points:**
    - Sliding window using HashSet: Lookup window is given as k. Means store only k size elements in set. If set size exceeds k then remove oldest element
    - Put each element in the set. If set already contains num, then duplicate is found
    - Add each num in set

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        
        HashSet<Integer> set = new HashSet<>();

        // Put each element in the set
        for (int i = 0; i < nums.length; i++) {
            // If set already contains num, then duplicate is found
            if (set.contains(nums[i])) {
                return true;
            }

            // Add each num in set
            set.add(nums[i]);

            // Lookup window is given as k. Means store only k size elements in set.
            // If set size exceeds k then remove oldest element
            if (set.size() > k) {
                set.remove(nums[i - k]);
            }
        }

        // If not found then return false
        return false;
    }
}
```