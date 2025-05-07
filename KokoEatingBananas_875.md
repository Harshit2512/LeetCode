- **Time Complexity:** O(n log(max(piles))), where log(max(piles)) is for the binary search and n for each check of canEatAllBananas.
- **Space Complexity:** O(1), using only a constant amount of extra space.
- **Key Points:**
    - Binary Search: find max pile (max speed in worst case), then find mid speed and increase or decrease speed based on how much hrs koko take to eat all banana
    - If more hrs needed, increase speed (find mid in right half), if less hrs needed, decrease speed (find mid in left half)

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        
        int maxPile = 0; // max speed needed in worst case

        for (int pile : piles) {
            maxPile = Math.max(maxPile, pile);
        }

        // Binary search pattern

        int left = 1; // min speed
        int right = maxPile; // max speed
        int resultedSpeed = maxPile;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (canEatAllBananas(piles, h, mid)) {
                resultedSpeed = mid; // at this speed, koko can eat all bananas
                right = mid - 1; // Try reduced spped
            } else {
                left = mid + 1; // try increased speed
            }
        }

        return resultedSpeed;
    }

    private boolean canEatAllBananas(int[] piles, int h, int speed) {
        int hoursNeeded = 0;

        for (int pile : piles) {
            hoursNeeded +=  (int) Math.ceil((double) pile/speed);
        }
        return hoursNeeded <= h;
    }
}
```