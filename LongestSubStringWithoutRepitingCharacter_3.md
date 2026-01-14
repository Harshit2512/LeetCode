- **Time Complexity:** O(N) - Interate all chars from string once
- **Space Complexity:** O(1) - No additional space
- **Approach:** ***Sliding window - Dynamic**
    - With Animation AM
    - Maintains the unique characters found in current substring
    - Start from left and right pointer at zero, keep moving right by checking if char is present in set.
    - If at right index, char is found in set then start removing all chars from left pointer until set doesn't have char found at right (appreantly duplicate char)
    - Add char at right pointer in set and find current maxLen of substring

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxLen = 0;
        int left = 0;
        Set<Character> set = new HashSet<>(); // maintains the unique characters found in current substring 

        for (int right = 0; right < s.length(); right++) {

            // If at right index, char is found in set then start removing all chars from left pointer until set doesn't have char found at right (appreantly duplicate char) and make fresh substring without having any duplicate

            while (set.contains(s.charAt(right))) { 
                set.remove(s.charAt(left));
                left++;
            }
            set.add(s.charAt(right));
            maxLen = Math.max(maxLen, right - left + 1);
        }

        return maxLen;
    }
}
```