### 485. Max Consecutive Ones

Given a binary array nums, return the maximum number of consecutive 1's in the array.

Example 1:

Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

### code :
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int count = 0;
        int longest = 0;

        for(int num : nums){
            if(num==1){
                count += 1;
            }else{
                count = 0;
            }

            longest = Math.max(longest,count);
        }
        return longest;
    }
}
```
Time Complexity: O(N), since we scan the array once.

Space Complexity: O(1), as only constant extra variables are used.


* it is optimal solution. if i want to  improve i will stop calling the math.max every iteration like this
* but the complexity remain same.
  
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int count = 0;
        int longest = 0;

        for (int num : nums) {
            if (num == 1) {
                count++;

                if (count > longest) {
                    longest = count;
                }
            } else {
                count = 0;
            }
        }

        return longest;
    }
}
```
