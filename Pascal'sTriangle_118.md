- **Time Complexity:** O(N * N), N is no of row and each row has N columns
- **Space Complexity:** O(1)
- **Approach:** SV, nCr, find element at given (row, col), (r-1)C(c-1)
    - For each row, generate element for column using (row - col) / col

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<>();

        for (int i=1; i <= numRows; i++) {
            // for each row, generate element for column
            List<Integer> temp = new ArrayList<>();
            int res = 1;
            // add 0th column as is
            temp.add(res);
            
            // for 0th based columns, start from 1st column
            for (int j = 1; j < i; j++) {
                res = res * (i - j); // numerator of nCr (row - col)
                res = res / j; // denomenator of nCr (col)
                temp.add(res);
            }

            result.add(temp);
        }

        return result;
    }
}

```