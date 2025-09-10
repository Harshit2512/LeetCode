- **Time Complexity:** O(N), where N is the length of the string, due to multiple in-place passes.
- **Space Complexity:** O(1), as modifications are performed in-place without extra space allocations outside of the input array.
- **Key Points:**
    - Use two pointers (one to track index of ch which needs to be moved and other to track the index of place where ch needs to be moved) to move chs within string in-place
    - Reverse the entire character array.
    - Reverse each word within the array.
    - Clean up any extra spaces resulting from the reversal process.

```java
class Solution {
    public String reverseWords(String s) {

        // Convert to to ch array
        char[] str = s.toCharArray();

        // Reverse string
        reverse(str, 0, str.length - 1);

        // Reverse words withing string
        reverseWord(str);

        // clean up spaces in string
        return cleanSpaces(str);
    }

    private void reverse(char[] s, int left, int right) {
        while (left < right) {
            char temp = s[left];
            s[left++] = s[right];
            s[right--] = temp;
        }
    }

    private void reverseWord(char[] s) {
        int n = s.length;
        int start = 0;

        for (int end = 0; end < n; end++) {
            // If index ch is space then reverse the word before it
            if (s[end] == ' ') {
                reverse(s, start, end - 1);
                start = end + 1; // set start index to first ch of next word
            }
        }

        // reverse last word
        reverse(s, start, n - 1);
    }

    private String cleanSpaces(char[] s) {
        int n = s.length;
        int i = 0, j = 0;

        while (j < n) {
            // Skip spaces
            while (j < n && s[j] == ' ') j++;
            // Move chars of words to appropriate next places
            while (j < n && s[j] != ' ') s[i++] = s[j++];

            // Skip the spaces come after words
            while (j < n && s[j] == ' ') j++;
            
            // Add one space after each word 
            if (j < n) s[i++] = ' ';  
        }

        return new String(s, 0, i);
    }
}
```