- **Time Complexity:** O(4^n / √n), This complexity is derived from the nth Catalan number, which is asymptotically equivalent to 4^n / √n.
- **Space Complexity:** O(n), The recursive stack has at most n stacks due to the maximum depth of recursion for valid combinations.
- **Key Points:**
    - Use backtracking method, and append '(' and ')' until given times and at each step backtrack

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, new StringBuilder(), 0, 0, n);
        return result;
    }

    private void backtrack(List<String> result, StringBuilder current, int open, int close, int n) {

        if (current.length() == 2 * n) {
            result.add(current.toString());
            return;
        }

        if (open < n) {
            current.append('(');
            backtrack(result, current, open + 1, close, n);
            current.deleteCharAt(current.length() - 1); // // Undo the last step (backtrack), prune the unnecessary path
        }

        if (close < open) {
            current.append(')');
            backtrack(result, current, open, close + 1, n);
            current.deleteCharAt(current.length() - 1);
        }
    }
}
```