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

## Better Aprroach :


### code :

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        // Store the size of the array
        int n = nums.length;

        // Return 0 if array is empty
        if (n == 0) return 0; 

        // Sort the array to bring consecutive numbers together
        Arrays.sort(nums); 

        // Variable to track the last smaller element in sequence
        int lastSmaller = Integer.MIN_VALUE; 

        // Variable to store the current sequence length
        int cnt = 0; 

        // Variable to store the longest sequence length found
        int longest = 1; 

        // Iterate through the sorted array
        for (int i = 0; i < n; i++) {
            // Case 1: Current element is exactly one greater than lastSmaller → part of sequence
            if (nums[i] - 1 == lastSmaller) {
                // Increment the sequence length
                cnt += 1; 
                // Update the last smaller element
                lastSmaller = nums[i]; 
            } 
            // Case 2: Current element is not consecutive and not a duplicate
            else if (nums[i] != lastSmaller) {
                // Reset the sequence length count to 1
                cnt = 1; 
                // Update the last smaller element
                lastSmaller = nums[i]; 
            }
            // Update the longest sequence length if the current sequence is longer
            longest = Math.max(longest, cnt); 
        }
        
        // Return the length of the longest consecutive sequence
        return longest;
    }
```

### complexity :

* Time complexity : o(n log n) + o(n)
* space complexity ; o(1)
