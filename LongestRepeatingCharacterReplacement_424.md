- **Time Complexity:** O(N) - iterate each char at most once
- **Space Complexity:** O(1) - Freq map is constant size
- **Approach:** ***Sliding Window - Dynami***
    - Maintain integer array for char's freq in current window
    - Calculate no of replacement needed by using length of current window and freq of char occoring most time
    - If no of replacement needed is greater than k then adjust window by increasing left pointer. Also reduce freq of removed char in integer array
    - Keep finding maxLen of valid window at each and return at last

``` java
class Solution {
    public int characterReplacement(String s, int k) {
        int maxCount = 0; // track freq of char occoring most in current window
        int left = 0;
        int maxLen = 0;
        int[] count = new int[26];

        for (int right = 0; right < s.length(); right++) {

            maxCount = Math.max(maxCount, ++count[s.charAt(right) - 'A']);

            // check validity for replacing by most k times
            int len = right - left + 1;
            if (len - maxCount > k) {
                // if condition is not valid, adjust window by increasing left pointer and also reduce freq of removed char
                count[s.charAt(left) - 'A']--;
                left++;
            }

            maxLen = Math.max(maxLen, right - left + 1);
        }

        return maxLen;
    }
}
```