
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

### Complexity :

* Time complexity : O(n^2)
* space Complexity : O(1)


## Better Solution :

Instead of checking all the conbinations for each element , we can store the elements with index in hashmap.
if target - nums[i] is found in the map, then nums[i] + map[need] == target, return their index.
by this we can traverse the array once to make O(n).

### algorithm :

* initialise the HashMap
* Run loop from i=0 to n.
* calculate Need = target - nums[i]
* check the conditiion ,  if(map.containsKey(Need) ---> if found,  retrurn  new int[]{i,map.get(Need)}.
* if false,   update the map with current num.   map.put[nums[i],i]
* retrun new int[]{}  , if combination does not exixst.

### Code :
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> mp = new HashMap<>();

        for(int i =0;i<nums.length;i++){
            
            int needed = target - nums[i];
            if(mp.containsKey(needed)){
                return new int[]{i,mp.get(needed)};
            }
            mp.put(nums[i],i);

        }   
        return new int[]{};
    }
}
```

### complexity :

* time complexity : O(n)
* space complexity : O(1)
  

