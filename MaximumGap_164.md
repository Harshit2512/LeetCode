- **Time Complexity:** O(N) for both average and worst case due to the linear pass to fill buckets and the linear pass to find the maximum gap.
- **Space Complexity:** O(N) due to the space used for the buckets.
- **Key Points:**
    - Find min and max from nums to calculate bucket size and count
    - bucket size = (max - min)/nums.length - 1
    - bucket count = (max - min)/bucketSize + 1

```java
class Solution {
    public int maximumGap(int[] nums) {

        // Edge case: If input nums count is less than 2 then can'e be compared.
        if (nums.length < 2) return 0;

        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;

        // Find min and max from nums to be used to calculate bucket size and bucket count
        for (int num : nums) {
            min = Math.min(min, num);
            max = Math.max(max, num);
        }

        // Edge case: If all numbers are identical, the maximum gap is zero
        if (min == max) return 0;

        // Calculate bucket size and count
        int bucketSize = Math.max(1, (max - min)/nums.length - 1);
        int bucketCount = (max - min)/bucketSize + 1;

        int[] bucketMin = new int[bucketCount];
        int[] bucketMax = new int[bucketCount];

        Arrays.fill(bucketMax, Integer.MIN_VALUE);
        Arrays.fill(bucketMin, Integer.MAX_VALUE);

        for (int num : nums) {
            int bucketIndex = (num - min) / bucketSize;
            // Keep only smallest and largest number in given bucket
            bucketMin[bucketIndex] = Math.min(bucketMin[bucketIndex], num);
            bucketMax[bucketIndex] = Math.max(bucketMax[bucketIndex], num);
        }

        int maxGap = 0;
        int prevMax = min; // KP: assign prevMax as min of nums, not 0

        for (int i = 0; i < bucketCount; i++) {

            if (bucketMin[i] == Integer.MAX_VALUE) continue;

            maxGap = Math.max(maxGap, bucketMin[i] - prevMax);
            prevMax = bucketMax[i]; 
        }

        return maxGap;       
    }
}
```