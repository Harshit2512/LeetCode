- **Time complexity:** O(N), N elements in array
- **Space complexity:** O(N), for hash map 
- **Approach: using prefix sum and hashmap (SV)**
    - subarrays in s-k = subarray can be made uptil current element
    - Maintain hashmap for prefix sum with frequency
    - Inital load for sum=0, sum 0 is always present and used for first subarray found
    - For current element, update prefix sum, find s-k: subarrays to be found in prefix sum
    - Increase subarray count if s-k is present in map, Update map for current prefix sum

```java

class Solution {
    public int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> hm = new HashMap<>();
        // inital load for sum=0, sum 0 is always present and used for first subarray found
        hm.put(0, 1);

        int pSum = 0;
        int cnt = 0;
       
        for (int i = 0; i < nums.length; i++) {
            // For current element, update prefix sum
            pSum += nums[i];

            // Find s-k: subarrays to be found in prefix sum
            int removal = pSum - k;

            // Increase subarray count if s-k is present in map
            if (hm.containsKey(removal)) {
                cnt += hm.get(removal);
            }

            // Update map for current prefix sum
            hm.put(pSum, hm.getOrDefault(pSum, 0) + 1);
        }

        // Total subarray found for sum k
        return cnt;
    }
}

```