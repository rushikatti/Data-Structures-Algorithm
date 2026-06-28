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
        for(int i=count0; i<count0 + count1 ;i++){
            nums[i] = 1;
        }
        for(int i=count0 + count1; i<nums.length; i++){
            nums[i] = 2;
        }
```

## Optimal solution -   Dutch National Flag algorithm.

Here instead of counting the 0 1 2 , will intialise the 3 pointers low, mid, high.  

* Intialise the pointer low & mid = 0, high = n -1.
* if nums[mid] == 0 , then swap with the nums[low] and increament the both.
* if nums[mid] == 1,  just move mid++,  there are already in place.
* else swap with low, move mid++ and high--.

```java
int low = 0, mid = 0, high = nums.length -1;

        while(mid <= high){
            if(nums[mid]==0){
                int temp = nums[mid];
                nums[mid] = nums[low];
                nums[low] = temp;
                low++;
                mid++;
            }
            else if(nums[mid]==1){
                mid++;
            }
            else{
                int temp = nums[mid];
                nums[mid] = nums[high];        
                nums[high] = temp;                 --> we should increament the mid here, because we don know
                high--;                                what value come from high after the swapping.

            }
        }
```


## Complexities :

* Time Complexity :  O(n)
* Space Complexity : O(1),  using the constant spaces for the counters.

These are same for all 3 approaches.
