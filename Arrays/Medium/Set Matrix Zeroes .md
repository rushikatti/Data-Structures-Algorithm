
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
* space complexity :  o(1)
