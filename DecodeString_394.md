- **Time Complexity:** O(n), where n is the length of the string. Each character is processed once.
- **Space Complexity:** O(n), used for the recursion stack and output string.
- **Key Points:**
    - Devide problem into sub-roblem for recursion
    - Build number k from series of digits 
    - recursive call for substrings
    - multiply letters within [] k times

```java
class Solution {

    private int index = 0;
    public String decodeString(String s) {

        // String to keep storing output from recursive calls
        StringBuilder result = new StringBuilder();
        
        // Read the string until character ']'
        while (index < s.length() && s.charAt(index) != ']') {
            
            char ch = s.charAt(index);

            // If char is digit, build the number from series of digits
            if (Character.isDigit(ch)) {
                int k = 0;
                
                // build number from sequence of digits
                while (index < s.length() && Character.isDigit(s.charAt(index))) {
                    k = k * 10 + (s.charAt(index) - '0');
                    index++;
                }
                index++; // skip character '['
                // call recursing function for sub-problem
                // sub string from recursive function
                String decodedSubString = decodeString(s);

                // multiply string k times and append to result
                while (k > 0) {
                    result.append(decodedSubString);
                    k--;
                }
                index++; // skip character ']'
            } else {
                // if current character is not digit then is character. Append to result string
                result.append(s.charAt(index));
                index++;
            }
        }

        return result.toString();
    }
}
```