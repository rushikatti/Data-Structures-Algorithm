## spiral printing of matrix

* for this problem there is only one approach.

* delcare left, right, top, bottom , and store the element in list


## code :

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int left = 0;
        int right = matrix[0].length -1;
        int top = 0;
        int bottom = matrix.length -1;

        List result = new ArrayList<>();

        while(left<=right && top<=bottom){

        for(int i= left;i<=right;i++){
            result.add(matrix[top][i]);
        }
        top++;

        for(int i=top;i<=bottom;i++){
            result.add(matrix[i][right]);
        }
        right--;

        if(top<=bottom){
            for(int i=right;i>=left;i--){
                result.add(matrix[bottom][i]);
            }
        }
        bottom--;

        if(left<=right){
            for(int i=bottom;i>=top;i--){
                result.add(matrix[i][left]);
            }
        }
        left++;

        }

        return result;
    }
}

```



### complexity :

* Time complexity : o(n * m)
* space complexity : o(n * m)




