
## Brute force solution 

we will traverse the matrix , if 0 is found then we will mark that row and col as -1
then we will traverse the matrix again replace -1 to 0

### code :

```java
class Solution {
    public void setZeroes(int[][] matrix) {

        int m = matrix.length;

        int n= matrix[0].length;

        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){

                    for(int col=0;col<n;col++){
                        if(matrix[i][col] != 0){
                            matrix[i][col] = -1;
                        }
                    }

                    for(int row=0;row<m;row++){
                        if(matrix[row][j] != 0){
                            matrix[row][j] = -1;
                        }
                    }
                }
            }
        }

        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==-1){
                    matrix[i][j] = 0;
                }
            }
        }
        
    }
}

```

### complexity :

* time complexity : (n * m)  +  (n + m) + ( n * m)  ,  so someware around the cube
* space complexity : O(1)

## Better approach :


* the idea is to keep track of row and col of the 0 found. to mark the entire row and col as zero after the second traversal.
* we will create row array and col array, and traverse the matrix if found 0. then we will mark the row[i] and col[j]  as true or 1.
* in second traversal , if row or col is true or 1 for that index then we will mark the index element as 0.


### code :

```java
class Solution {
    public void setZeroes(int[][] matrix) {

        int m = matrix.length;

        int n= matrix[0].length;
        
        boolean[] row = new boolean[m];

        boolean[] col = new boolean[n];


        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){

                    row[i] = true;
                    col[j] = true;
                }
            }
        }



        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(row[i] || col[j]){
                    matrix[i][j] = 0;
                }
            }
        }
        
    }
}
```



### complexity :

* Time complexity :  (n*m) + (n*m)  ,  someware around n2
* space complexity :  o(n) + o(m)



## Optimal solution :

* Instead of using separate arrays, we use the first row and first column of the matrix itself to store whether a row or column needs to be zeroed. We also store two flags:
*firstRowZero:Was the first row supposed to be all zero?
*firstColZero:Was the first column supposed to be all zero?

*Then:
* First pass: Mark zeros in the first row and column for any zero found in the rest of the matrix.
* Second pass: Use those markers to set rows and columns to zero.
* Finally, handle the first row and column separately based on the flags. This is super space-efficient because we’re reusing the input matrix itself to store markers.


* Check if the first row has any zero and store in a boolean flag.
* Check if the first column has any zero and store in a boolean flag.
* Traverse the rest of the matrix:
* If a cell is zero, mark its row in the first column and its column in the first row as zero.
* Traverse again (excluding first row and column), setting cells to zero if their row marker or column marker is zero.
* Finally, update the first row and first column based on the stored flags.


### code :

```java
class Solution {
    public void setZeroes(int[][] matrix) {

        int m = matrix.length;

        int n= matrix[0].length;
        
        boolean firstrowzero  = false;

        boolean firstcolzero = false;

        for(int j=0;j<n;j++){
            if(matrix[0][j]==0){
                firstrowzero = true;
                break;
            }
        }
        
        for(int i=0;i<m;i++){
            if(matrix[i][0]==0){
                firstcolzero = true;
                break;
            }
        }

        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(matrix[i][j]==0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(matrix[i][0] == 0 || matrix[0][j]==0){
                    matrix[i][j] = 0;
                }
            }
        }

        if(firstrowzero){
            for(int j=0;j<n;j++){
                matrix[0][j] = 0;
            }
        }
        if(firstcolzero){
            for(int i=0;i<m;i++){
                matrix[i][0] = 0;
            }
        }
    }
}
```

### complexity :

* time complexity : o(n * m)
* space complexity : o(1)
