* problem : return the majority element which appeared more than n/3 times.

## bruteforce :

run 2 loops and count each element . if the count is > n/3 and ans list does not have the num. update the ans list with that num.

### code :

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {

        List<Integer> ans = new ArrayList<>();

        for(int i=0;i<nums.length;i++){
            int count = 0;
            for(int j=0;j<nums.length;j++){
                if(nums[j]==nums[i]){
                    count++;
                }
            }
            if(count > nums.length/3 && !ans.contains(nums[i])){
                ans.add(nums[i]);
            }
        }return ans;
        
    }
}
```

### Complexity :

* time complexity : O(n^2)
* space complexity : O(1)
  
