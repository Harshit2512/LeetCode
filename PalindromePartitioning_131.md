- **Time Complexity:** O(n * 2^n), where n is the length of the string. This complexity is due to the fact that each character might either start its own substring or extend a previous one, leading to exponential possibilities.
- **Space Complexity:** O(n), where n is the depth of the recursion. The space is used by the recursive call stack.
- **Key Points:**
    - Take index and check if palindrom, if yes then make partition and keep repeating process for substring taking single char, two char,...until last char

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(s, 0, result, new ArrayList<>());
        return result;
    }

    private void backtrack(String s, int start, List<List<String>> result, List<String> current) {
        // Base case: If start index is equal to end of the string then add current to result
        if (start == s.length()) {
            result.add(new ArrayList<>(current));
            return;
        }

        // From start index, start checking if char at index and then substring is palindrom or not
        for (int end = start; end < s.length(); end++) {

            if (isPalindrome(s, start, end)) {
                // If palindrom then add substring to current and then backtrack
                current.add(s.substring(start, end + 1));
                backtrack(s, end + 1, result, current);
                current.remove(current.size() - 1); // undo last choice
            }
        }
    }

    private boolean isPalindrome(String s, int left, int right) {

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```