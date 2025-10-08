- **Time Complexity:** O(N), where N is the number of elements in nums. This is because we are only doing constant-time operations per element.
- **Space Complexity:** O(N) for storing the frequency map and bucket list.
- **Key Points:**
    - Approach : Bucket Sort technique since the maximum frequency of any element can't exceed the number of elements
    - Build the frequency map.
    - Create buckets where index corresponds to frequency, and append elements to respective buckets.
    - Iterate from the end of the bucket array to pick the top k frequent elements.

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        
        // Use hash map for frequency count
        // Count frequency of eack element using hash map
        HashMap<Integer, Integer> freq = new HashMap<>();

        for (int num : nums) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }

        // Create list of integer array to perform bucket sort
        // We can utilize a bucket sort technique since the maximum frequency of any element can't exceed the number of elements.
        // Put num at it's frequency indexed element in list
        List<Integer>[] freqBucket = new List[nums.length + 1];

        for (int key : freq.keySet()) {
            int frequency = freq.get(key);

            // If bucket is not present then create bucket(array) first
            if (freqBucket[frequency] == null) {
                freqBucket[frequency] = new ArrayList();
            }

            // Diff num with same frequency can go in same bucket element
            freqBucket[frequency].add(key);
        }

        // Result integer array of size k
        int[] topK = new int[k];
        int index = 0;

        // Since max freq element goes farther at index in array, start iterating from end
        for (int i = freqBucket.length - 1; i >= 0 && index < k; i--) {
            if (freqBucket[i] != null) {
                for (int num : freqBucket[i]) {
                    // Access bucket element and put in result array untill k
                    topK[index++] = num;
                    if (index == k) {
                        break;
                    }
                }
            }
        }

        return topK;
    }
}
```