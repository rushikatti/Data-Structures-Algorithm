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
  

## Better Solution :

instead of 3 loops, we can use 2 loop and count the sum in the second loop and make the solution in O(n^2).

### algorithm :

* Run outer loop i
* intialise the sum variable
* run inner loop j and add the sum += nums[j].
* return the maxSum.

### code :

```java
class Solution {
    
    public int maxSubArray(int[] nums) {
        int maxi = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
            
            int sum = 0; 

            for (int j = i; j < nums.length; j++) {
                sum += nums[j];
                maxi = Math.max(maxi, sum);
            }
        }
        return maxi;
    }
}
```

### Complexity :

* Time complexity :  O(n^2)
* Space complexity : O(1)
  



