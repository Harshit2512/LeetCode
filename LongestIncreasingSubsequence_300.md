- **Time Complexity:** O(n log n), due to binary searching within tails for each of the n elements.
- **Space Complexity:** O(n), used for the tails array.


```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int[] tails = new int[nums.length];

        Arrays.fill(tails, 1);
        int size = 0;

        for (int num : nums) {
            int left = 0, right = size;

            while (left < right) {
                int mid = left + (right - left)/2;

                if (tails[mid] < num) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }

            tails[left] = num;
            if (left == size) size++;
        }

        return size;
    }
}
```