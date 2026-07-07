## Brute force

traverse the array and swap matrix[i][n-1-i] = matrix[i][j]

### code :

```java
class Solution {
    // Function to rotate the matrix 90 degrees clockwise using extra space
    public int[][] rotateClockwise(int[][] matrix) {
        // Get the size of the square matrix
        int n = matrix.length;

        // Create a new matrix of same size to store rotated result
        int[][] rotated = new int[n][n];

        // Traverse each element of original matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                // Place the element at its new rotated position
                rotated[j][n - i - 1] = matrix[i][j];
            }
        }

        // Return the rotated matrix
        return rotated;
    }
}

```

### complexity :

* Time complexity : o(n^2)
* space complexity : o(n^2)


## optimal solution :

we will transpose the matrix and reverse the each row 

### code :

```java
