
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
