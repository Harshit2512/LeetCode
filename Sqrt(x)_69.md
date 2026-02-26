// Time Complexity: O(log N), Binary Search
// Space Complexity: O(1)
// Approach: Clue: answer range is known in advance (ans can't exceed x), Hence BS can be used
//  - For x = 0 and 1, ans will be x itself
//  - If sqr(mid) < x, All smaller numbers than mid can't be answer, so eliminate left half of numbers
//  - If sqr(mid) > x, All greater numbers than mid can't be answer, so eliminate right half of numbers

```java 

class Solution {
    public int mySqrt(int x) {
        // Clue: answer range is known in advance (ans can't exceed x), Hence BS can be used
        int low = 1;
        int high = x / 2;
        //int ans = 1;

        // For x = 0 and 1, ans will be x itself
        if (x < 2) return x;  

        while (low <= high) {

            int mid = (low + high) / 2;
            long square = (long) mid * mid;

            if (square == x) {
                return mid;
            } else if (square < x) {
                //ans = mid;
                // All smaller numbers than mid can't be answer, so eliminate left half of numbers
                low = mid + 1;
            } else {
                // If sqr(mid) > x, All greater numbers than mid can't be answer, so eliminate right half of numbers
                high = mid - 1;
            }
        }

        //return ans;
        return high;
        
    }
}

```