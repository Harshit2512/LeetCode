- **Time Complexity:** O(N!) - In the worst-case scenario, every queen has N possible options to place.
- **Space Complexity:** O(N) - Used for storing the sets and board state.
- **Key Points:**
    - iterate each col for given row to see if queen is safely placed
    - queen moves diagonally, straight vertically (in col) and horizontally (in row), check that other queen is not already placed at these positions
    - place the queen at current row and col and backtrack

```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        
        Set<Integer> cols = new HashSet<>(); // To check ig queen is placed in the col
        Set<Integer> posDiags = new HashSet<>(); // To main all positive diagonals
        Set<Integer> negDiags = new HashSet<>(); // To main all negative diagonals
        List<List<String>> result = new ArrayList<>(); // result board configurations
        char[][] board = new char[n][n];

        for (int i = 0; i < n; i++) {
            Arrays.fill(board[i], '.');
        }

        backtrack(0, cols, posDiags, negDiags, board, result, n);
        return result;
    }

    private void backtrack(int row, Set<Integer> cols, Set<Integer> posDiags, Set<Integer> negDiags, char[][] board, List<List<String>> result, int n) {

        // Base case: if iterated all rows then add current board config in result 
        if (row == n) {
            result.add(construct(board));
            return;
        }

        // iterate each col for given row to see if queen is safely placed
        for (int col = 0; col < n; col++) {
            int posDiag = row + col; // row + col sum is constant for all diagonals
            int negDiag = row - col; // row - col sum is constant for all diagonals

            // queen moves diagonally, straight vertically (in col) and horizontally (in row)
            // check that other queen is not already placed at these positions
            if (cols.contains(col) || posDiags.contains(posDiag) || negDiags.contains(negDiag)) {
                continue;
            }
            
            // place the queen at current row and col and backtrack
            cols.add(col);
            posDiags.add(posDiag);
            negDiags.add(negDiag);
            board[row][col] = 'Q';
            backtrack(row + 1, cols, posDiags, negDiags, board, result, n);
            cols.remove(col);
            posDiags.remove(posDiag);
            negDiags.remove(negDiag);
            board[row][col] = '.';
        }
    }

    private List<String> construct(char[][] board) {
        List<String> path = new ArrayList<>();
        for (char[] row : board) {
            path.add(new String(row)); // Convert char array (row) to string
        }
        return path;
    }
}
```