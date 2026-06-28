# Sorting the 0s 1s 2s :

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

## 1)  Brute force :

* intialise the counters for the 0 1 and 2.
* Traverse the array and increment the respective counts.
* intialise the index = 0, to fill the given array.
* fill the array with while loops with condition
``` while(count0-- >0){
        nums[index++] = 0;
    while(count1-- >0){
        nums[index++] = 1;
    while(count2-- >0){
        nums[index++] = 2;
    }
```

### code :
``` java
class Solution {
    public void sortColors(int[] nums) {
        int count0 = 0, count1=0, count2=0;

        for(int num: nums){
            if(num == 0){
                count0++;
            }else if(num == 1){
                count1++;

            }else{
                count2++;
            }
        }
        int index = 0;

        while(count0-- > 0){
            nums[index++] = 0;
        }
        while(count1-- > 0){
            nums[index++] = 1;
        }
        while(count2-- >0){
            nums[index++] = 2;
        }
       
    }
}
```

## Better Solution :

Instead of while loop with index pointer.  use for loops with i pointer
``` java

        for(int i=0;i<count0;i++){
            nums[i] = 0;
        }
        for(int i=count0;i<count0+count1;i++){
            nums[i] = 1;
        }
        for(int i=count1; i<nums.length; i++){
            nums[i] = 2;
        }
```

