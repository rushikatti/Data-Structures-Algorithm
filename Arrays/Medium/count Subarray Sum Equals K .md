
# Count Subarray Sum Equals K

## Brute force :

* 3 loops
  
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

* 2 loops

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


## Optimal Solution :

* prefix sum approach

### code :

```java
class Solution {
    public int subarraySum(int[] nums, int k) {

        HashMap<Integer,Integer> map = new HashMap<>();

        map.put(0,1);

        int prefixSum = 0;
        int count = 0;

        for(int i=0;i<nums.length;i++){
            prefixSum += nums[i];

            int need = prefixSum - k;

            if(map.containsKey(need)){
                count += map.get(need);
            }

            map.put(prefixSum,map.getOrDefault(prefixSum,0)+1);
        }

        return count;
    }
}
```


### Complexity :

* time complexity : o(n)
* space complexity : o(n)


