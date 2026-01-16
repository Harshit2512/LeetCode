- **Time complexity** = O(n^2), where n is the number of rows (or columns) in the matrix.
- **Space complexity** = O(1)
- https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/rotate-image.md
- **Approach:**
    - Transpose of matrix --> transform [i][j] to [j][i] (cross element swap) using 2 for loops
    - Reverese the matrix --> transfer each row element (left and right columns elements swap) in reverse order

```java

class Solution {
    public void rotate(int[][] matrix) {

        int n = matrix.length;

        // transpose of matrix --> transform [i][j] to [j][i] using 2 for loops
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // reverese the matrix --> transfer each row element in reverse order (use start and end pointer and swap elements)
        for (int i = 0; i < n; i++) {
            int start = 0;
            int end = n - 1;

            while (start < end) {
                int temp = matrix[i][end];
                matrix[i][end] = matrix[i][start];
                matrix[i][start] = temp;
                start++;
                end--;
            }
        }
    }
}

```