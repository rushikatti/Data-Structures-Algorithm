# Longest Consecutive Sequence :

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

## Brute force :

i will pick each element and do linear search to find the next element if exist i willl increment the count

### algoritm :

* create the linear search function  linearSearch(int[] arr, int num)
* in longest subsequence method, intialise the longest = 1
* loop the nums, and declare x = nums[i] and count = 1
* while(linearSearch(nums,x+1)==true) , x = x+1, count = count + 1.
* return the longest

### code :

```java
Longest Consecutive Sequencclass Solution {

    public boolean linearSearch(int[] arr, int num ){
        for(int i=0;i<arr.length;i++){


            if(arr[i]==num){
                return true;
            }
        }
        return false;
    }
    public int longestConsecutive(int[] nums) {

        int longest = 1;

        if(nums.length==0){
            return 0;
        }

        for(int i=0;i<nums.length;i++){
            int x = nums[i];

            int count = 1;

            while(linearSearch(nums,x+1)==true){
                x += 1;
                count +=1;
            }

            longest = Math.max(longest,count);
        }
        return longest;
    }
}
```

### complexity 

* Time complexity : O(n)*o(n) --> o(n^2)
* space complexity : o(1)
