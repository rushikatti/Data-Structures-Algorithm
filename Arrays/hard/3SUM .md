
# 3SUM :

## Brute force solution :

* Run 3 loops, i with 0, j with i+1, k with j+1.
* add i+j+k == 0,  store them in temp List
* sort the temp list before adding to the Set<List<>>
* return new ArrayList<>(Set).


## Better Solution :

* run two loops, i with 0, j with i+1
* calculate third element = -(nums[i] + nums[j]),
* check  third in  HASHSET if found , add i , j, third to temp LIST , and sort it before adding to Set.
* eturn new ArrayList<>(Set).



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


### Better Solution code :

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
    

    Set<List<Integer>> ans = new HashSet<>();
      
        int n = nums.length;
        for(int i=0;i<n;i++){
            Set<Integer> hashset = new HashSet<>();
            for(int j=i+1;j<n;j++){

                int third = -(nums[i]+nums[j]);

                if(hashset.contains(third)){
                    List<Integer> temp = Arrays.asList(nums[i],nums[j],third);
                    Collections.sort(temp);
                    ans.add(temp);

                }
            hashset.add(nums[j]);
            }
        }
        return new ArrayList<>(ans);        
    }
}
        

```

### complexity :

* time : O( n ^2 + log( num pf triplets))
* space : O( 2 * no of unique triplets )

  
