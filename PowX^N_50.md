**Time Complexity:** O(log n): Recursive function halves n at each call.
**Space Complexity:** O(log n): Call stack space for recursion.
**Key Points:**
    - dividing the problem size by half at each step, leading to a more efficient solution.
    - if n % 2 == 1, means n is odd. So multiply result with addition x

```java
class Solution {

    // Approach: Recursive Approach with Divide and Conquer 
    public double myPow(double x, int n) {

        if (n == 0) return 1; 

        if (n < 0) {
            x = 1/x;
            n = -n;
        }

        return findPower(x, n);
    }

    private double findPower(double x, int n) {

        if (n == 0) return 1;
        double halfResult = findPower(x, n/2);

        if (n % 2 == 0) {
            return halfResult * halfResult;
        } else {
            return x * halfResult * halfResult;
        }
    }   


// ------------------------------------------------------------------------------------------------------------------------------------------------------
        // // Approach: Iterative Binary Exponentiation (Optimal) using bit manipulation to identify N is odd or not
        // // Time Complexity: O(log n): The powering operation uses logarithmic number of multiplications.
        // // Space Complexity: O(1): This approach does not use additional space.

        // long N = n;

        // // If n < 0, perform op on x and n to revere
        // if (N < 0) {
        //     x = 1/x;
        //     N = -N;
        // }

        // double currentProduct = x;
        // double result = 1;
        
        // // Iterate while there's still power to consider
        // while (N > 0) {
        //     // If N is odd, multiply result by current product
        //     if (N % 2 == 1) {
        //         result *= currentProduct;
        //     }

        //     currentProduct *= currentProduct;
        //     N = N / 2;
        // }

        // return result;
        
    //}
    
}
```