
# 3SUM :

## Brute force solution :

* Run 3 loops, i with 0, j with i+1, k with j+1.
* add i+j+k == 0,  store them in temp List
* sort the temp list before adding to the Set<List<>>
* return new ArrayList<>(Set).



### Bruteforce code :

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
    

    Set<List<Integer>> ans = new HashSet<>();
      
        int n = nums.length;
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                for(int k=j+1;k<n;k++){
                    if(nums[i]+nums[j]+nums[k]==0){
                        List<Integer> temp = Arrays.asList(nums[i],nums[j],nums[k]);
                        Collections.sort(temp);
                        ans.add(temp);
                    }
                }
            }
        }
        return new ArrayList<>(ans);
    }
}
        

```

### complexity :

* Time : O(n^3 * log( No of triplets) )
* space : O(2 * no of triplets)            --> storing the set and List.
