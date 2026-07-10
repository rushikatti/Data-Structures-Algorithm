# Majority Element 1

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

## BruteForce solution :

### algorithm :
* run outer loop
* intialise the count=0, run inner loop to check the count of each i.
* if nums[i]==nums[j] , count++
* after 1 iteration,  if(count > n/2)  return nums[i].


## Optimal Solution :

** Moors mayer Algorithm. **
```
* Initialize four variables: cnt1 and cnt2 for tracking the counts of elements, and el1 and el2 for storing the potential majority elements.
*Traverse through the given array:
    If cnt1 is 0 and the current element is not equal to el2, set el1 to the current element and increment cnt1 by 1.
    If cnt2 is 0 and the current element is not equal to el1, set el2 to the current element and increment cnt2 by 1.
    If the current element is equal to el1, increment cnt1 by 1.
    If the current element is equal to el2, increment cnt2 by 1.

*In all other cases, decrease cnt1 and cnt2 by 1.
*After processing all elements, el1 and el2 should be the candidate elements for majority. To confirm:
*Use another loop to manually check the counts of el1 and el2 in the array.
    If either el1 or el2's count is greater than floor(N/3), it is considered a valid majority element.
```
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

* Time complexity : O(N) + O(N log N),      n logn for tarverse the array and store in map,  o(n) to traverse the map.
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


### Optimal code :

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {

    int count1 = 0;
    int element1 = Integer.MIN_VALUE;

    int count2 = 0;
    int element2 = Integer.MIN_VALUE;

    for(int i=0;i<nums.length;i++){
        if(count1 == 0 && nums[i] != element2){
            count1 =1;
            element1 = nums[i];
        }
        else if(count2 == 0 && nums[i] != element1){
            count2=1;
            element2 = nums[i];
        }
        else if(nums[i] == element1){
            count1++;
        }
        else if(nums[i] == element2){
            count2++;
        }
        else{
            count1--;
            count2--;
        }
    }

    int cnt1 =0, cnt2=0;

    for(int i=0;i<nums.length;i++){
        if(nums[i] == element1) cnt1++;
       if(nums[i] == element2) cnt2++;
    }

    int min = (nums.length / 3) + 1;
    List<Integer> ans = new ArrayList<>();
    if(cnt1 >= min) ans.add(element1);
    if(cnt2 >= min && element1 != element2) ans.add(element2);

    return ans;

    }
}
```

### Complexity :

* time complexity : O(2n)
* space complexity : O(1)
