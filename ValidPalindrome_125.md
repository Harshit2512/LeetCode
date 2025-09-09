- **Time Complexity:** O(n), where n is the length of the input string. We traverse each character at most twice.
- **Space Complexity:** O(1), no additional space is used beyond integer indices.
- **Key Points:**
    - Two pointers approach (left and right)
    - While left is less than right: Increment the left pointer until an alphanumeric character is found.
    - Decrement the right pointer until an alphanumeric character is found.
    - Compare the characters. If they are not equal, the string is not a palindrome.
    - Move the pointers inward and repeat.
    - If the entire string is processed without mismatches, it is a palindrome

```java
class Solution {
    public boolean isPalindrome(String s) {
        // Start left index from 0 and right index from end of string
        int start = 0;
        int end = s.length() - 1;

        while (start < end) {
            // If ch at start index is not alpha-numeric then keep increasing start until comes alpha-numeric ch
            while (start < end && !Character.isLetterOrDigit(s.charAt(start))) start++;

            // If ch at end index is not alpha-numeric then keep decreasing end until comes alpha-numeric ch
            while (start < end && !Character.isLetterOrDigit(s.charAt(end))) end--;

            // If lowercase ch at start and end index don't match then string is not palindrom
            if (Character.toLowerCase(s.charAt(start)) != Character.toLowerCase(s.charAt(end))) {
                return false;
            }

            // If ch at start and end index match then increase start and decrease end index
            start++;
            end--;
        }

        // Return true, means string is palindrom
        return true;
    }
}
```