- **Time Complexity:** O(N^2), where N is the length of the grid's side. In the worst case, we might check each cell to determine if a section is uniform.
- **Space Complexity:** O(log(N)), as the stack space used by the recursive calls at worst will be log of N due to the depth of the recursive tree.
- **Key Points:**
    - Find if the matrix/sub-matrix is uniform
    - If not uniform, break it into half and perform recursion and create children nodes

```java
class Solution {
    public Node construct(int[][] grid) {
        return constructQuad(grid, 0, 0, grid.length);
    }

    public Node constructQuad(int[][] grid, int row, int col, int size) {
        // Break condition in recursion, creating leaf node 
        if (isUniform(grid, row, col, size)) {
            return new Node(grid[row][col] == 1, true);
        }

        // Divide matrix into half and find children
        int mid = size/2;

        Node topLeft = constructQuad(grid, row, col, mid);
        Node topRight = constructQuad(grid, row, col + mid, mid);
        Node bottomLeft = constructQuad(grid, row + mid, col, mid);
        Node bottomRight = constructQuad(grid, row + mid, col + mid, mid);

        // Once all 4 children nodes for res quadrants are created, create a parent node
        return new Node(false, false, topLeft, topRight, bottomLeft, bottomRight);

    }

    public boolean isUniform(int[][] grid, int row, int col, int size) {

        int val = grid[row][col];
        for (int i = row; i < row + size; i++) {
            for (int j = col; j < col + size; j++) {
                if (grid[i][j] != val) {
                    return false;
                }
            }
        }
        return true;
    }
}
```