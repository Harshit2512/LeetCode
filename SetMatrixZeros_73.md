https://www.youtube.com/watch?v=dSxt3ZCbIqA
https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/set-matrix-zeroes.md
**Time complexity** = O ( 3 * m * n) ~= O(m * n)
    - We need to iterate matrix elements  3 times
    - 1st, when setting first row and col flag value set
    - 2nd, when setting zero for respective row and col by terating elemets and checking if [r][c] = 0
    - 3rd, when setting 0 to [r][c] by looking up if first row ([0][c]) or col ([0][c]) is 0
**Space complexity** = O(1), no addition space taken
**Approach**:
    - Step 1: First check if 0 present is any element of first row or col, if present then mark that row or col as true for making all 0
    - Step 2: 0 setting for first row and col wrt to element: Start iterating from row=1, col=1, and if [r][c]=0 then set 0 in that perticular first row and first col
    - Step 3: 0 setting for [r][c] element if [0][c] or [r][0] is 0 


```java

class Solution {
    public void setZeroes(int[][] matrix) {

        boolean firstRowZero = false;
        boolean firstColZero = false;
        int rows = matrix.length;
        int cols = matrix[0].length;


        // Determine if first row and column will need zeroing 
        for (int r = 0; r < rows; r++) {
            if (matrix[r][0] == 0) {
                firstColZero = true;
                break;
            }
        }
        
        for (int c = 0; c < cols; c++) {
            if (matrix[0][c] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Use first row and column as markers and set 0 by checking other matrix elements
        for (int r = 1; r < rows; r++) {
            for (int c = 1; c < cols; c++) {
                if (matrix[r][c] == 0) {
                    matrix[0][c] = 0;
                    matrix[r][0] = 0;
                }
            }
        }

        // Set matrix zeroes using markers (update 0 in elements by looking at 0 in first row and column)
        for (int r = 1; r < rows; r++) {
            for (int c = 1; c < cols; c++) {
                if (matrix[r][0] == 0 || matrix[0][c] == 0) {
                    matrix[r][c] = 0;
                }
            }
        }

        // Zero first column if needed
        if (firstColZero) {
            for (int r = 0; r < rows; r++) {
                matrix[r][0] = 0;
            }
        }

        // Zero first row if needed
        if (firstRowZero) {
            for (int c = 0; c < cols; c++) {
                matrix[0][c] = 0;
            }
        }       
    }
}

```