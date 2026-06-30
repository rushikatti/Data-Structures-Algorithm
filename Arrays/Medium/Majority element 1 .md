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


## Better approach :

Use HashMap , store the frequency of elements , traverse the map to find value > n / 2.

### algorithm :

* Initialise the HashMap
* Run the loop and count frequency of each element
* traverse the map   Map.Entry<Integer,Integer> entry = new entrySet()
* check if(entry.getValue() > n/2) , if true return entry.getKey() else return -1.

### code :
```java
class Solution {
  
    public int majorityElement(int[] nums) {  
        int n = nums.length;      
        HashMap<Integer, Integer> map = new HashMap<>();
    
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
                
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() > n / 2) {
                return entry.getKey();
            }
        }
        return -1;
    }
}
```

### complexity :

* Time complexity : O(N) + O(N log N)
* space complexity : O(N)


## Optimal Solution :

** Moors Voting Algorithm **

this will find the majority element by taking 1st element and increment count if next element equal to 1st else decrement the count.
once count become 0, it will take next element as 1st and do the same process. if count is positive at the end that willl be the majority element.

###  algorithm :

* Initialize two variables: count to track the count of elements, and element to keep track of the element being counted.
* Traverse through the given array. If count is 0, store the current value of the array as element.
* If the current element in the array is the same as element, increment the count by 1.
* If the current element is different from element, decrement the count by 1.
* At the end of the traversal, the integer stored in element will be the expected result (the majority element).

### code :

```java
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        int element = 0;

        for(int i=0;i<nums.length;i++){
            if(count == 0){
            count = 1;
            element = nums[i];
            }
            else if(element == nums[i]){
                count++;
            }
            else{
                count--;
            }
        }
        int count2 = 0;
        for(int num : nums){
            if(num==element){
                count2++;
            }
        }

        if(count2 > nums.length / 2){
            return element;
        }

        return -1;
    }
}
```

### Complexity :

* Time complexity : O(n)
* space complexity : O(1)
