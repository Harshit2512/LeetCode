- **Time Complexity:** O(n + m), where n is the length of s and m is the length of t.
- **Space Complexity:** O(1), no additional space is used.
- **Key Points:**
    - Two pointers approach, define index i and j for string s and t respectively
    - Iterate both strings, if char at index matches then increament both index else increament only t string index
    - If value of s string index i is equal to length of s then it's subsequence, all characters of s were found in t 

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        // Set pointers to 0
        int i = 0, j = 0;

        while (i < s.length() && j < t.length()) {
            if (s.charAt(i) == t.charAt(j)) {
                i++;
                j++;
            } else {
                j++;
            }
        }

        // If value of i is equal to length of s then it's subsequence, all characters of s were found in t
        return i == s.length();
    }
}
```