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
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        for(int i=0;i<n;i++){                                   ---->  transpose of matrix
            for(int j=i+1;j<n;j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        for(int i=0;i<n;i++){
            int left = 0;
            int right = n-1;

            while(left <right){
                int temp = matrix[i][left];                        ----> reversing each row
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
        
    }
}
```


### complexity :

* Time complexity : o(n^2)
* space complexity : o(1)


