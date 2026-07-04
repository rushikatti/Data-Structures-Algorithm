
# Count Subarray Sum Equals K

## Brute force :

### code :

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        for(int i=0;i<nums.length;i++){
            for(int j=i;j<nums.length;j++){
                int sum = 0;
                for(int r=i;r<=j;k++){
                    sum += nums[r];
                }
                if(sum==k){
                    count++;
                }
            }
        }
        return count;
    }
}
```

### Complexity :

* time complexity : o(n^3)
* space complexity : o(1)

## Better approach 

### code :
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        for(int i=0;i<nums.length;i++){
            int sum = 0;
            for(int j=i;j<nums.length;j++){
                sum += nums[j];
               
                if(sum==k){
                    count++;
                }
            }
        }
        return count;
    }
}
```


### Complexity :

* time complexity : o(n^2)
* space complexity : o(1)




