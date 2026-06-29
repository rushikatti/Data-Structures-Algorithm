
## Two Sum :

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

* So there are two varients, 
1) return true / false,  if two number exist equal to the target.
2) Return the [i,j] of the two numbers equal to target.

## Brute Force :

* run outer loop for all the elements.
* run the inner loop to add every element with i.
* if nums[i] + nums[j] == target,  return new int[]{i,j}.

### code :
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i =0;i<nums.length;i++){
            for(int j=0;j<nums.length;j++){                        j=0 will take 92 ms to run, 
                if(i==j){                                          so start with j = i + 1 to get 45 ms
                    continue;
                }
                if(nums[i]+nums[j]==target){
                    return new int[]{i,j};
                }
            }
        }
       return new int[]{}; 
    }
}
```
* j = i + 1, do not compare the already compared index so this will be faster
[1,2] , [2,1]  both are same, we can skin one.
