- **Time Complexity:** O(m * n), where m is the number of rows and n is the number of columns, as we might need to visit every cell.
- **Space Complexity:** O(m * n) due to the recursion stack.
- **Key Points:**
    - Reverse thinking approach 
    - (DFS) - Capture unsurrounded region from first and last rows and cols (O -> #)
    - Uncapture unsurrounded region on border (# -> O) and surrounded regions (O -> X)

```java
class Solution {
    public void solve(char[][] board) {

        if (board == null || board.length == 0) return;
        
        int rows = board.length;
        int cols = board[0].length;

        // Iterate first and last rows to check if any un-sorrounded region and replace O
        for (int i = 0; i < rows; i++) {
            if (board[i][0] == 'O') dfs(board, i, 0);
            if (board[i][cols - 1] == 'O') dfs(board, i, cols - 1); 
        }

        // Iterate first and last cols to check if any un-sorrounded region and replace O
        for (int j = 0; j < cols; j++) {
            if (board[0][j] == 'O') dfs(board, 0, j);
            if (board[rows - 1][j] == 'O') dfs(board, rows - 1, j); 
        }

        // Visit all cells and replace sourrrounded region ceel with X and unsourrounded region cells (on border) with O (from #)
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                else if (board[i][j] == '#') board[i][j] = 'O'; 
            }
        }
    }

    private void dfs(char[][] board, int i, int j) {
        // Boundary condition to check if out of bound
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] != 'O') {
            return;
        }

        // Replace with # temporary
        board[i][j] = '#';

        // Move in all directions
        dfs(board, i - 1, j);
        dfs(board, i + 1, j);
        dfs(board, i, j + 1);
        dfs(board, i, j - 1);

    }
}
```