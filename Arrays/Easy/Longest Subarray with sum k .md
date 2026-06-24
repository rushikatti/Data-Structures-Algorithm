### Longest subarray with sum k :

#### Bruteforce :
```
We can solve using the 3 loops 
* one outer loop
* one inner loop
* one loop to count the sum of inner loop
```
```java
import java.util.*;

class Solution {

    public int longestSubarray(int[] nums, int k) {
        int n = nums.length;
        int maxLength = 0;

        // starting index
        for (int startIndex = 0; startIndex < n; startIndex++) {
            // ending index
            for (int endIndex = startIndex; endIndex < n; endIndex++) {

                /* add all the elements of
                   subarray = nums[startIndex...endIndex] */
                int currentSum = 0;
                for (int i = startIndex; i <= endIndex; i++) {
                    currentSum += nums[i];
                }

                if (currentSum == k) {
                    maxLength = Math.max(maxLength, endIndex - startIndex + 1);
                }
            }
        }
        return maxLength;
```
    }
}
