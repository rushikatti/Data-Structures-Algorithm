
```
                1
              1   1
            1   2   1
          1   3   3   1
        1   4   6   4   1
      1   5  10  10   5   1
    1   6  15  20  15   6   1
  1   7  21  35  35  21   7   1
1   8  28  56  70  56  28   8   1

```

##  Problem type 1 :

* the question will provide the row and col number , we have to return  the element in that position

### Solution :
```
n              n!
 C    =  ----------------
  r        r! * (n-r)!
```

* i should run the lopp untill the r! , and remaining will cancle out

### code :

```
func(r-1,n-1){

res = 1

for(int i=0;i<r;i++){
res = res * (n-i);
res = res / (i+1);
}
return res;
}
```

### complexity :

* Time complexity :   O(r)
* space complexity : O(1)

## problem 2 :

* The question will give the numRows i have to print pascal triangle.

### solution :

For each row:

* The first and last elements are always 1.
* Every middle element is the sum of the two elements above it.
* Use the previous row to generate the current row.

### code :

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {

        List<List<Integer>> ans = new ArrayList<>();

        for(int i=0;i<numRows;i++){
            List<Integer> row = new ArrayList<>();

            for(int j=0;j<=i;j++){
                if(j==0 || j==i){
                    row.add(1);
                }else{
                    row.add(ans.get(i-1).get(j-1) + ans.get(i-1).get(j));
                }
            }
            ans.add(row);
        }
        return ans;
    }
}
```

### complexity :

* Time complexity = o(n^2)
* space complexity = O(n^2)



