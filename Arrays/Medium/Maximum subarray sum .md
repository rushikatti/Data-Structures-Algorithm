# Maximum Subarray Sum 

## Brute force :

for every element i, explore al the elements using j , traverse the subarray i to j add the sum. return the max sum

* this will trigger time limit exceeeded error.

### algorithm :

* run outer loop
* run inner lop j from i to n
* intialise the sum = 0
* run loop from i to j and add the sum

### code :
```java
class Solution {
   
    public int maxSubArray(int[] nums) {
            
        int maxi = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
                     
            for (int j = i; j < nums.length; j++) {
             
                int sum = 0;
     
                for (int k = i; k <= j; k++) {
                    sum += nums[k];
                }
                maxi = Math.max(maxi, sum);
            }
        }
        return maxi;
    }
}
```

### Complexity :

* Time complexity :  O(n^3)
* Space complexity : O(1)
* 
