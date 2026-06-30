# Majority Element 1

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

## BruteForce solution :

### algorithm :
* run outer loop
* intialise the count=0, run inner loop to check the count of each i.
* if nums[i]==nums[j] , count++
* after 1 iteration,  if(count > n/2)  return nums[i].

### code :
```java
class Solution {
    public int majorityElement(int[] nums) {
        for(int i=0;i<nums.length;i++){
            int count = 0;
            for(int j=0;j<nums.length;j++){
                if(nums[i]==nums[j]){
                    count++;
                }              
            }
             if(count > nums.length/2){
                    return nums[i];
            }
        }
        return -1;
    }
}
```

### complexity :

* time complexity : o(N^2)
* space complexity : o(1)
