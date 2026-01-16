- Video explanation - https://www.youtube.com/watch?v=BJnMZNwUk1M
- https://github.com/AlgoMaster-io/leetcode-solutions/blob/main/java/spiral-matrix.md
- **Time complexity** = O(m * n), where m is the number of rows and n is the number of columns. Every element in the matrix is visited exactly once
- **Space complexity** = O(1), excluding the space used by the output list
- **Approach:**: 
    - Traverse matrix using left, right, top and bottom pointers to traverse rows and cols with boundries
    - If conditions (left <= right) and (top <= bottom) to detemine to traverse only if more than one col and row respectively

```java

class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        
        List<Integer> result = new ArrayList<>();

        int left = 0;
        int right = matrix[0].length - 1;
        int top = 0;
        int bottom = matrix.length - 1;

        if (matrix == null || matrix.length == 0) {
            return result;
        }

        while (left <= right && top <= bottom) {
            for (int i = left; i <= right; i++) {
                result.add(matrix[top][i]);
            }
            top++;

            for (int j = top; j <= bottom; j++) {
                result.add(matrix[j][right]);
            }
            right--;

            // If condition? --> In case where there is only one row, diff between top and
            // bottom gives no of rows (check presence of row)
            if (top <= bottom) {
                for (int k = right; k >= left; k--) {
                    result.add(matrix[bottom][k]);
                }
                bottom--;
            }

            // If condition? --> In case where there is only one column, diff between left
            // and right gives no of columns (check presence of column)
            if (left <= right) {
                for (int l = bottom; l >= top; l--) {
                    result.add(matrix[l][left]);
                }
                left++;
            }
        }
        return result;
    }
}

```java